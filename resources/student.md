Student
=======

A student is the primary object to make requests using the API, without one, you can't make any calls.

API resources
-----------------

* [Properties](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#properties)
* [Status Codes](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#status-codes)
* [Endpoints](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#endpoints)
    * [Get student](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#get-studentid)
    * [Create student](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#post-student)
    * [Edit student](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#post-studentid)
    * [Create friendship](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#post-studentfriendshipcreate)
    * [Delete friendship](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#post-studentfriendshipdelete)
    * [Send message](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#post-studentmessagecreate)
    * [Get messages](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#get-studentmessagegetid)
    * [Send wink](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#post-studentwinkcreate)
    * [Get winks](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#get-studentwinkget)
    * [Create group](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#post-studentgroupcreate)
    * [Send group message](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#post-studentgroupidsend_message)
    * [Get group messages](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#get-studentgroupidget_message)
    * [Invite group](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#post-studentgroupidinvite)
    * [Leave group](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#post-studentgroupidleave)
    * [List conversation](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md#get-studentlist_conversations)

Properties
----------

| Property        | Explanation                                                                                                                                        |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| id              | The unique numeric identifier for the Student                                                                                                      |
| name            | The name of the student                                                                                                                            |
| email           | The email of the student                                                                                                                           |
| phone_number    | The phone number of the student                                                                                                                    |
| country         | The country of the student (The default is Brazil)                                                                                                 |
| created_at      | Date when the student was created (in "YYYY-MM-DD HH:MM:SS" format)                                                                                |
| last_seen       | Date when the student was last seen (in "YYYY-MM-DD HH:MM:SS" format)                                                                              |
| user_hash       | The hash used to make requests (see more in [authentication](https://github.com/brunocordeiro/school_api/blob/master/resources/authentication.md)) |
| is_athletic     | If the student belongs to an athletic.                                                                                                             |
| is_superuser    | If the student have superuser privileges.                                                                                                             |
| facebook_id     | The ID used for facebook.                                                                                                                          |

Status Codes
------------

| Status    | Explanation                            |
| --------- | -------------------------------------- |
| 1         | Missing required field.                |
| 2         | Email is not valid.                    |
| 3         | Invalid Country ID.                    |
| 4         | Invalid University ID.                 |
| 5         | Email already exists.                  |
| 6         | There is no student with such ID.      |
| 7         | Do not have permission.                |
| 8         | The student is not active anymore.     |
| 9         | Students are already friends.          |
| 10        | Students are not friends.              |
| 11        | Empty message.                         |
| 12        | Invalid group name.                    |
| 13        | Not enough students.                   |
| 14        | Group does not exist.                  |
| 15        | Student is not a member of this group. |
| 16        | Student already in the group.          |
| 17        | Student not in the group.              |


Endpoints
---------

### GET /student/#{id}

Receive a single user.

#### GET /student/5670

Ok example

`HTTP/1.1 200 OK`

```json
{
    "student_created_at": "2015-03-20 15:34:43",
    "student_id": 5670,
    "student_phone_number": "",
    "student_country": {
        "country_name": "Brasil",
        "country_name_es": "Brazil",
        "country_id": 1,
        "country_name_en": "Brasil",
    },
    "done": true,
    "error": false,
    "user_last_seen": "2015-04-13 21:34:51",
    "message": "",
    "student_name": "My Name",
    "student_email": "email@email.com",
    "status_code": 200,
    "student_hash": "1fd0ebe770238f56c59cd44197c82ec7763dcad21377b48bb60b99be",
}
```

#### GET /student/5671

Error example

`HTTP/1.1 200 OK`

```json
{
    "user_created_at": "",
    "user_id": "",
    "user_phone_number": "",
    "user_country": "",
    "done": false,
    "error": true,
    "user_last_seen": "",
    "message": "There is no student with such ID.",
    "user_name": "",
    "user_email": "",
    "status_code": 6,
    "thumbnail_image": "",
    "large_image": "",
    "user_hash": "",
}
```
### POST /student

Creates a new student.

#### Required Fields

| Property       | Explanation                                                                                                                           |
| -------------- | ------------------------------- |
| name           | The name of the student         |
| password       | The password of the student     |
| email          | The email of the student        |


#### Optional Fields

| Property       | Explanation                                                                                                                          |
| -------------- | ------------------------------------------------------------------- |
| country_id     | The ID of the country of the student (The default is Brazil)        |
| university_id  | The ID of the university of the student (The default is Sao Judas)  |
| phone_number   | The phone number of the user                                        |

#### Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "message": "",
    "done": true,
    "user_hash": "1fd0ebe770238f56c59cd44197c82ec7763dcad21377b48bb60b99be",
    "status_code": 200,
}
```

#### Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "message": "Email already exists.",
    "done": false,
    "user_hash": "",
    "status_code": 5,
}
```

### POST /student/#{id}

Edit a existing student.

#### Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "message": "",
    "done": true,
    "user_hash": "1fd0ebe770238f56c59cd44197c82ec7763dcad21377b48bb60b99be",
    "status_code": 200,
}
```

#### Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "message": "Email already exists.",
    "done": false,
    "user_hash": "",
    "status_code": 5,
}
```

### POST /student/friendship/create

Create a new friendship between two students.

#### Required Fields

| Property       | Explanation                                                                                                                           |
| -------------- | ----------------------------------------- |
| student_id     | The ID of the student to add as friends.  |

#### Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "message": "",
    "done": true,
    "status_code": 200,
}
```

#### Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "message": "Students are already friends.",
    "done": false,
    "status_code": 9,
}
```

### POST /student/friendship/delete

Delete a friendship between two students.

#### Required Fields

| Property       | Explanation                                                                                                                           |
| -------------- | ----------------------------------------- |
| student_id     | The ID of the student to add as friends.  |

#### Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "message": "",
    "done": true,
    "status_code": 200,
}
```

#### Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "message": "Students are not friends.",
    "done": false,
    "status_code": 10,
}
```

### GET /student/friendship/get

Get a list of friends from the student (in alphabetical order).

#### Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "message": "",
    "done": true,
    "status_code": 200,
    "friend_list": [
        {
            "friend_id": 4,
            "friend_name": "Jefferson",
        },
        {
            "friend_id": 3,
            "friend_name: "Roberson",
        },
    ],
}
```

#### Error example

This function does not fail (it is not supposed to).

### POST student/message/create

Send a message to a friend student.

#### Required Fields

| Property       | Explanation                                                                                                                           |
| -------------- | ------------------------------------------ |
| student_id     | The ID of the student to send the message. |
| contents       | The contents of the message.               |

#### Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "message": "",
    "done": true,
    "status_code": 200,
}
```

#### Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "message": "Empty message.",
    "done": false,
    "status_code": 11,
}
```

### GET student/message/get/#{id}

Get the messages between two students (new messages first).

#### Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "message": "",
    "done": true,
    "status_code": 200,
    "message_list": [
        {
            "created_at": "2015-03-24 21:59:00",
            "sender": 1,
            "contents": "Tudo sim."
        },
        {
            "created_at": "2015-03-24 21:57:00",
            "sender": 4,
            "contents": "Olar. Tudo bom?",
        },
    ],
}
```

#### Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "message": "There is no student with such ID.",
    "done": false,
    "status_code": 6,
    "message_list": [],
}
```

### POST student/wink/create

Send a wink to a student.

#### Required Fields

| Property       | Explanation                                                                                                                           |
| -------------- | ------------------------------------------ |
| student_id     | The ID of the student to send the wink.    |

#### Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "message": "",
    "done": true,
    "status_code": 200,
}
```

#### Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "message": "There is no student with such ID.",
    "done": false,
    "status_code": 6,
}
```

### GET student/wink/get

Get the winks the student has received (new ones first).

#### Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "message": "",
    "done": true,
    "status_code": 200,
    "wink_list": [
        {
            "created_at": "2015-03-24 21:59:00",
            "sender": 4,
        },
        {
            "created_at": "2015-03-24 21:57:00",
            "sender": 3,
        },
    ],
}
```

#### Error example

This function does not fail (it is not supposed to).

### POST student/group/create

Creates a new group of students.

#### Required Fields

| Property       | Explanation                                                                                                                           |
| -------------- | --------------------------------------------------------------------------------------- |
| group_name     | The name of the group to be created.                                                    |
| student_list   | The list of students to be invited to the group (comma separeted, example: "4,7,32,77") |

#### Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "message": "",
    "done": true,
    "status_code": 200,
    "group_id": 4,
    "group_name": "Nois que voa bruxao!",
}
```

#### Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "message": "Not enough students.",
    "done": false,
    "status_code": 13,
    "group_id": 0,
    "group_name": "",
}
```

### POST student/group/#{id}/send_message

Sends a message to a group.

#### Required Fields

| Property       | Explanation                                                                                                                           |
| -------------- | ----------------------------- |
| contents       | The contents of the message.  |

#### Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "message": "",
    "done": true,
    "status_code": 200,
}
```

#### Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "message": "Empty message.",
    "done": false,
    "status_code": 11,
}
```

### GET student/group/#{id}/get_message

Get messages from a group (new messages first).

#### Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "message": "",
    "done": true,
    "status_code": 200,
    "message_list": [
        {
            "created_at": "2015-03-24 21:59:00",
            "sender": 4,
            "contents": "Opa."
        },
        {
            "created_at": "2015-03-24 21:57:00",
            "sender": 3,
            "contents": "Olar."
        },
    ],
}
```

#### Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "message": "Student is not a member of this group.",
    "done": false,
    "status_code": 15,
    "message_list": [],
}
```

### POST student/group/#{id}/invite

Invite a student to a group (only the person who created the group can do that).

#### Required Fields

| Property       | Explanation                                                                                                                           |
| -------------- | ------------------------------------- |
| student_id     | The ID of the student to be invited.  |

#### Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "message": "",
    "done": true,
    "status_code": 200,
}
```

#### Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "message": "Do not have permission.",
    "done": false,
    "status_code": 7,
}
```

### POST student/group/#{id}/leave

Leave a group.

#### Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "message": "",
    "done": true,
    "status_code": 200,
}
```

#### Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "message": "Student not in the group.",
    "done": false,
    "status_code": 17,
}
```

### GET student/list_conversations

List all conversations a student participates (conversations and groups).
The conversation with the last message shows first.

#### Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "message": "",
    "done": true,
    "status_code": 200,
    "conversation_list": [
        {
            "last_message": "Blz.",
            "student_id": 4,
            "conversation_time": "2015-03-24 21:59:00",
            "conversation_name": "Jefferson",
            "last_message_from": "Cordeiro",
            "group_id": 0,
        },
        {
            "last_message": "Nois.",
            "student_id": 0,
            "conversation_time": "2015-03-24 21:55:00",
            "conversation_name": "Nois que voa bruxao!",
            "last_message_from": "Roberson",
            "group_id": 1,
        },
        {
            "last_message": "Joia.",
            "student_id": 3,
            "conversation_time": "2015-03-24 21:54:00",
            "conversation_name": "Roberson",
            "last_message_from": "Roberson",
            "group_id: 0,
        },
    ],
}
```

#### Error example

This function does not fail (it is not supposed to).