Feed
=======

A student is the primary object to make requests using the API, without one, you can't make any calls.

API resources
-----------------

* [Properties](https://github.com/brunocordeiro/school_api/blob/master/resources/feed.md#properties)
* [Status Codes](https://github.com/brunocordeiro/school_api/blob/master/resources/feed.md#status-codes)
* [Endpoints](https://github.com/brunocordeiro/school_api/blob/master/resources/feed.md#endpoints)


Properties
----------

| Property        | Explanation                                                                                                                                        |
| --------------- | --------------------------------------------- |
| id              | The unique numeric identifier for the Feed    |
| university      | The university which the feed belongs         |
| is_athletic     | The type of the feed                          |

Status Codes
------------

| Status    | Explanation                            |
| --------- | -------------------------------------- |
| 7         | Do not have permission.                |
| 30        | Invalid university ID.                 |
| 31        | Invalid feed ID.                       |
| 32        | Invalid topic ID.                      |
| 33        | Already liked/disliked.                |
| 34        | Already reported.                      |
| 35        | Invalid comment ID.                    |


Endpoints
---------

### GET /feed/#{feed_type}/#{id}

Get the topics from a feed.
The feed_type can be "athletic" or "regular".
The id is the id of the university.
New topics will appear first.

Ok example

`HTTP/1.1 200 OK`

```json
{
    "topic_list": [
        {
            "created_at": "2015-04-07 19:21:41",
            "comments": 0,
            "deslikes": 0,
            "likes": 0,
            "topic_id": 3,
            "contents": "Olar.",
        },
        {
            "created_at": "2015-04-07 19:20:08",
            "comments": 0,
            "deslikes": 0,
            "likes": 0,
            "topic_id": 2,
            "contents": "Quem vai na festa amanha?",
        },
        {
            "created_at": "2015-04-07 19:19:32",
            "comments": 2,
            "deslikes": 1,
            "likes": 0,
            "topic_id": 1,
            "contents": "Quem topa uma breja hj???",
        },
    ],
    "status_code": 200,
    "done": true,
    "feed_dict": {
        "feed_university_id": 1,
        "feed_type": "regular",
        "feed_id": 2,
        "feed_university_name": "Sao Judas",
    },
    "error": false,
    "message": "",
}
```

Error example

`HTTP/1.1 200 OK`

```json
{
    "topic_list": [],
    "status_code": 30,
    "done": false,
    "feed_dict": {},
    "error": true,
    "message": "Invalid university ID.",
}
```

### POST /feed/topic/create

Create a new topic.

#### Required Fields

| Property       | Explanation                                                                                                                           |
| -------------- | -------------------------------------------------- |
| university_id  | The ID of the university the topic will belong to. |
| contents       | The contents of the topic.                         |

Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "done": true,
    "message": "",
    "status_code": 200,
    "topic_id": 47,
}
```

Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "done": false,
    "message": "Do not have permission.",
    "status_code": 7,
    "topic_id": 0,
}
```

### GET /feed/topic/#{id}

Get the comments from a topic.

Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "done": true,
    "message": "",
    "status_code": 200,
    "comment_list": [
        {
            "student_id": 1,
            "created_at": "2015-04-07 19:48:15",
            "likes": 1,
            "student_name": "Bruno",
            "dislike": 0,
            "contents": "La no bar do lado.",
        },
        {
            "student_id": 1,
            "created_at": "2015-04-07 19:57:18",
            "likes": 0,
            "student_name": "Bruno",
            "dislike": 0,
            "contents": "Ninguem topa?",
    },
    "topic_dict": {
        "topic_student_name": "Bruno",
        "topic_dislikes": 1,
        "topic_created_at": "2015-04-07 19:19:32",
        "topic_student_id": 1,
        "topic_id": 1,
        "topic_contents": "Quem topa uma breja hj???",
        "topic_likes": 0,
    },
}
```

Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "done": false,
    "message": "Invalid topic ID.",
    "status_code": 32,
    "topic_dict": {},
    "comment_list": [],
}
```

### POST /feed/topic/#{id}/delete

Deletes a topic.

Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "done": true,
    "message": "",
    "status_code": 200,
}
```

Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "done": false,
    "message": "Do not have permission.",
    "status_code": 7,
}
```

### POST /feed/topic/#{id}/like

Likes a topic.

Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "done": true,
    "message": "",
    "status_code": 200,
}
```

Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "done": false,
    "message": "Invalid topic ID.",
    "status_code": 32,
}
```

### POST /feed/topic/#{id}/dislike

Dislikes a topic.

Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "done": true,
    "message": "",
    "status_code": 200,
}
```

Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "done": false,
    "message": "Invalid topic ID.",
    "status_code": 32,
}
```

### POST /feed/topic/#{id}/report

Report a topic.

Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "done": true,
    "message": "",
    "status_code": 200,
}
```

Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "done": false,
    "message": "Invalid topic ID.",
    "status_code": 32,
}
```

### POST /feed/topic/#{id}/create_comment

Create a new comment in a topic.

#### Required Fields

| Property       | Explanation                                                                                                                           |
| -------------- | -------------------------------------------------- |
| contents       | The contents of the comment.                       |

Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "done": true,
    "message": "",
    "status_code": 200,
}
```

Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "done": false,
    "message": "Invalid topic ID.",
    "status_code": 32,
}
```

### POST /feed/topic/comment/#{id}/delete

Delete a comment.

Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "done": true,
    "message": "",
    "status_code": 200,
}
```

Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "done": false,
    "message": "Invalid comment ID.",
    "status_code": 35,
}
```

### POST /feed/topic/comment/#{id}/like

Like a comment.

Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "done": true,
    "message": "",
    "status_code": 200,
}
```

Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "done": false,
    "message": "Invalid comment ID.",
    "status_code": 35,
}
```

### POST /feed/topic/comment/#{id}/dislike

Dislike a comment.

Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "done": true,
    "message": "",
    "status_code": 200,
}
```

Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "done": false,
    "message": "Invalid comment ID.",
    "status_code": 35,
}
```

### POST /feed/topic/comment/#{id}/report

Report a comment.

Ok example

`HTTP/1.1 200 OK`

```json
{
    "error": false,
    "done": true,
    "message": "",
    "status_code": 200,
}
```

Error example

`HTTP/1.1 200 OK`

```json
{
    "error": true,
    "done": false,
    "message": "Invalid comment ID.",
    "status_code": 35,
}
```