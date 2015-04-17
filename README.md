API Documentation
====================

This is a REST-style API that uses JSON for serialization and OAuth 2 for authentication.

Where do I start?
----------------

Want to get started with API integration? Here's a quick check list:

1. Read up on [how to authenticate](#authentication) to learn how to make api calls.
2. Read the API docs to understand what you can do with your app.

Making a request
----------------

All URLs start with `http://localhost:8000/`.

For example:
To make a request to get the student with id equals 1, you would do the following in curl:

```shell
curl -i -H 'content-type: application/json' -H 'accept: application/json' \
  --user ACCESS_TOKEN:x http://localhost:8000/student/1
```

where `ACCESS_TOKEN` is the user's access token (see Authentication).


Authentication
--------------

We follow the OAuth 2 framework for letting users authorize your application to use our API on their behalf. Quite briefly, when you create a new user you will obtain an access token (a secret string denoting your rights over this user), which you have to include in the header of every request (as shown in the above example).

Read the [authentication guide](https://github.com/brunocordeiro/school_api/blob/master/resources/authentication.md) to get started.

Just JSON
-----------------

All data is sent and received as JSON. Our format is to have no root element and we use snake\_case to describe attribute keys. This means that you have to send `Content-Type: application/json` when POSTing data into our API.

You'll receive a `415 Unsupported Media Type` response code if you leave out the `Content-Type` header.

API resources
-----------------

* [Student](https://github.com/brunocordeiro/school_api/blob/master/resources/student.md)
* [Feed](https://github.com/brunocordeiro/school_api/blob/master/resources/feed.md)
* [Event](https://github.com/brunocordeiro/school_api/blob/master/resources/event.md)