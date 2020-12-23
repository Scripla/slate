---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='http://app.scripla.com'>Sign Up for an Account</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

This is a very early version of the external Scripla API. The endpoints may change without notice. Please contact support@scripla.com with any questions. Examples given here are just examples and will take some tweaking to work for your specific needs.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass Basic Auth with each request
curl "api_endpoint_here" \
  -H "Authorization: meowmeowmeow"
```

> Make sure to use your real user name and password.

Scripla allows for partial access to it's data via API endpoints. For most usages you can simply pass in BASIC HTTP Authorization using your user name and password.

`curl --basic --user user@example.com:m4p@55w0rd http://app.scripla.com/users/1.json
`

<aside class="notice">
You must use your user name and password from your account. Make sure to properly set accepts headers. Currently we can return data in JSON.
</aside>

# Users

## Get A User's Information

```shell
curl --basic --user user@example.com:m4p@55w0rd http://app.scripla.com/users/1.json
```


> The above command returns JSON structured like this:

```json
{
    "id":1,
    "login":"coteyr@coteyr.net",
    "name":"Robert Cotey",
    "email":"coteyr@coteyr.net",
    "created_at":"2020-10-14T21:46:50.000Z",
    "updated_at":"2020-12-23T19:50:42.000Z",
    "remember_token":null,
    "remember_token_expires_at":null,
    "first_name":"Robert",
    "last_name":"Cotey",
    "avatar":{
        "url":"/default_avatar.png",
        "small":{"url":"/default_avatar.png"},
        "mid":{"url":"/default_avatar.png"},
        "large":{"url":"/default_avatar.png"}
    },
    "user_type":"explorer",
    "profile_photo":{
        "url":null,
        "small":{"url":null},
        "mid":{"url":null},
        "large":{"url":null}
    },
    "bible_id":1,
    "birthday":null,
    "admin":false,
    "vetted":true
}

```

This endpoint retrieves a single users information. There is no way to return a list of all users.

### HTTP Request

`GET /users/:id`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
id | false | The id if the user to retrieve


<aside class="success">
You will only be able to see users that you (the logged in user) would otherwise be able to see. There is no call to see all users, instead use this call along with the contributions to get that profiles details.
</aside>

## Create a user (sign up)

```shell
curl http://app.scripla.com/users.json \
--form "user[passsword]=demopass"  \
--form "user[bible_id]=1" \
--form "user[user_type]=explorer" \
--form "user[email]=apidemo1@scripla.com" \
--form "user[avatar_new]=@/home/coteyr/P1000086.JPG" \
--form "user[last_name]=User" \
--form "user[first_name]=Test" \
--form "user[password_confirmation]=demopass"

```


> The above command returns JSON structured like this on failure:

```json
{
    "password":["can't be blank","is too short (minimum is 6 characters)"],
    "password_confirmation":["can't be blank"],
    "login":["can't be blank","is too short (minimum is 3 characters)","use only letters, numbers, and .-_@ please."],
    "first_name":["can't be blank"],
    "last_name":["can't be blank"],
    "avatar_new":["must supply an avatar"],
    "bible_id":["can't be blank"],
    "email":["can't be blank","should look like an email address.","is too short (minimum is 6 characters)"],
    "bible":["must exist"],
    "user_type":["can't be blank","is not included in the list"]}

```
> The above command returns JSON structured like this on success:

```json
{
    "id":8,
    "login":"apidemo1@scripla.com",
    "name":"Test User",
    "email":"apidemo1@scripla.com",
    "created_at":"2020-12-23T22:00:37.000Z",
    "updated_at":"2020-12-23T22:00:37.000Z",
    "remember_token":null,
    "remember_token_expires_at":null,
    "first_name":"Test",
    "last_name":"User",
    "avatar":{
        "url":"/default_avatar.png",
        "small":{"url":"/default_avatar.png"},
        "mid":{"url":"/default_avatar.png"},
        "large":{"url":"/default_avatar.png"}
    },
    "user_type":"explorer",
    "profile_photo":{
        "url":null,
        "small":{"url":null},
        "mid":{"url":null},
        "large":{"url":null}
    },
    "google_auth":null,
    "bible_id":1,
    "birthday":null,
}

```
It's important to store the user's ID locally, other then logging back in there is no way to get the id again. 

### HTTP Request

`POST /users/`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
password|null|
bible_id|null|set to 1|
user_type|null|explorer or creator
email|null| 
password|null| 
password_confirmation|null|must match password
avatar_new|null|any image type, square is better



<aside class="warning">
Make sure to store the user id locally, the id will not be presented again. 
</aside>


