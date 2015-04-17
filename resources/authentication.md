We provide authorization and user authentication by a restricted form of BasicAuth. In a glance:
- The only grant type we support is the "authorization code" one.
- Our access tokens don't expire. They become invalid only if the user removes his/her profile from the app.

Authorization flow
------------------

The authorization flow is pretty standard:

1. The user creates a new user through the app, or connect using facebook.
2. Your app will send a POST to the server, so it can create the new user.
3. If everything is ok, the server will answer with a `user_hash` code.
4. You will use this `user_hash` code in every request you make in the future.

#### Example

Asume that you want to create the following user:
 - Name =  My Name
 - E-mail = email@em.com
 - password = 1234567

Then you will do:

```shell
curl -i -H 'content-type: application/json' -H 'accept: application/json' \
  --data 'name=My Name&email=email2@em.com&password=1234567' \
  http://localhost:8000/student
```

And you will recieve (if everything is ok):

`HTTP/1.0 200 OK`
`Content-Type: application/json`

```json
{
    "message": "",
    "done": true,
    "user_hash": "fafc20162ea06b14c697cf9c90b6a3e6e8bc2c0f0592307f03627033",
    "error": false,
    "status_code": 200
}
```

And now you will store the `user_hash` and use it in the future requests.
When creating the BasicAuth token, the login will not be used and the password will be the `user_hash`.