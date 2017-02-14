# OP api documentation
OP Project api documentation


# Getting Started
## login
to send a login request and get your token, send a request to this url, and set needed x-www-form-urlencoded data.
[http://armandar.com/api/v1/login](http://armandar.com/api/v1/login)

add this header to your request:
```
    key: Content-Type
    value: application/x-www-form-urlencoded
```

and send this data:
```json
  "data": {
    "grant_type": "password",
    "username": "username",
    "password": "password"
  }
```