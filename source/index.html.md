---
title: Ride-My-Way

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Ride-My-Way is a web carpooling app. It offers affordable rides to different destination in nigeria.

The API provides a secured means of creating and managing ride offers.

`BASE URL:` `https://still-basin-40207.herokuapp.com/api/v1`

# Authentication

An Authentication is required to access features of the system. Login or Register to get a token which will allow you access other features of the system

The App expects all request to the server to include a token in the header as `x-access-token` or as a query string `req.query` 

`http://app_url?token=the_string_of_token`

<aside class="notice">
You must replace <code>the_string_of_token</code> with your personal token.
</aside>

# User

## Create Account
Creates a new User

### HTTP Request
* Endpoint `auth/signup`
* Verb `POST`
* Body `(application/json)`

### HTTP Response
* Status Code `201`
* Body `(application/json)`

> Request Body

```json
{
  "user":   {
    "name": "Travis Node",
    "email": "travis@node.com",
    "phone": 080123456789,
    "password": "secret",
    "confirm": "secret"
  }
}
```

> Response Object

```json
{
  "status": "success",
  "message": "User registered succesfully",
  "user":   {
    "id": 1,
    "name": "Travis Node",
    "email": "travis@node.com",
    "phone": 080123456789
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MTEsIm5hbWUiOiJLaW5nc2xleSBNaWNoZWFsIiwiaWF0IjoxNTMwNzc5MTI0LCJleHAiOjE1MzA4NjU1MjR9.wKwd2jAd0wktlNTyZV76guJDqEyi0o6q9ICCpHproo4"
}
```


## Login

> Request Body

```json
{
  "user": {
    "email": "travis@node.com",
    "password": "secret"
  }
}
```

> Response Object

```json
{
  "status": "success",
  "message": "Login Succesful",
  "user":   {
    "id": 1,
    "name": "Travis Node",
    "email": "travis@node.com",
    "phone": 080123456789
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MTEsIm5hbWUiOiJLaW5nc2xleSBNaWNoZWFsIiwiaWF0IjoxNTMwNzc5MTI0LCJleHAiOjE1MzA4NjU1MjR9.wKwd2jAd0wktlNTyZV76guJDqEyi0o6q9ICCpHproo4"
}
```

This endpoint logs in a user

### HTTP Request
* Endpoint `auth/login`
* Verb `POST`
* Body `(application/json)`

### HTTP Response
* Status Code `200`
* Body `(application/json)`


# Ride

## Create Ride
Creates a new ride offer

### HTTP Request
* Endpoint `/users/rides`
* Verb `POST`
* Body `(application/json)`
* Require Token: `true`

### HTTP Response
* Status Code `200`
* Body `(application/json)`

> Request Body

```json
{
  "ride":   {
    "location": "ESlint Way",
    "destination": "Airbnb",
    "date": "12/02/2018",
    "time": "12:30",
    "price": 2000
  }
}
```

> Response Object

```json
{
    "status": "success",
    "message": "Ride Offer Created Succesfully",
    "data": {
        "id": 11,
        "location": "Port Harcourt",
        "destination": "Eslint Way",
        "date": "01/08/2018",
        "time": "12:30",
        "creator_id": 11,
        "creator_name": "Kingsley Micheal"
    }
}
```


## Get All Ride
Get all available ride offer

### HTTP Request
* Endpoint `/rides`
* Verb `GET`
* Body `(application/json)`
* Require Token: `true`

### HTTP Response
* Status Code `200`
* Body `(application/json)`
```

> Response Object

```json
{
    "status": "success",
    "data": {
        "rides": [
            {
                "id": 1,
                "userid": 1,
                "location": "Oshodi",
                "destination": "Yaba",
                "date": "12/12/2018",
                "time": "12:00",
                "price": 1500
            },
            {
                "id": 2,
                "userid": 2,
                "location": "Port Harcourt",
                "destination": "Abuja",
                "date": "12/11/2018",
                "time": "12:30",
                "price": 7500
            },
            {
                "id": 3,
                "userid": 2,
                "location": "Owerri",
                "destination": "Lagos",
                "date": "10/11/2018",
                "time": "12:30",
                "price": 7500
            }
        ]
    }
}
```

## Get A Ride
Get a specify ride

### HTTP Request
* Endpoint `/rides/:id`
* Verb `GET`
* Body `(application/json)`
* Require Token: `true`

### HTTP Response
* Status Code `200`
* Body `(application/json)`

> Response Object

```json
{
    "status": "success",
    "data": {
        "rides": [
            {
                "id": 1,
                "userid": 1,
                "location": "Oshodi",
                "destination": "Yaba",
                "date": "12/12/2018",
                "time": "12:00",
                "price": 1500
            }
        ]
    }
}
```

## Request A Ride
Request to join a ride offer. A user cannot request a ride he/she created

### HTTP Request
* Endpoint `/rides/:id/requests`
* Verb `POST`
* Body `(application/json)`
* Require Token: `true`
* `id`: `rides id`

### HTTP Response
* Status Code `201`
* Body `(application/json)`

> Response Object

```json
{
  "status": "success",
  "message": "Ride requested succesfully"
}
```

## View Ride Request
User can view request to the ride he/she created

### HTTP Request
* Endpoint `users/rides/:id/requests`
* Verb `GET`
* Body `(application/json)`
* Require Token: `true`
* `id`: `rides id`

### HTTP Response
* Status Code `200`
* Body `(application/json)`

> Response Object

```json
{
    "status": "success",
    "data": [
        {
            "id": 9,
            "rideid": 9,
            "userid": 11,
            "status": "Requested",
            "notification": null
        }
    ]
}
```

## Respond To Request
User can respond to ride request by providing a status of 'Accepted' or 'Rejected'

### HTTP Request
* Endpoint `users/rides/:rideId/requests/:requestId`
* Verb `PUT`
* Body `(application/json)`
* Require Token: `true`
* `rideId`: `rides id`
* `requestId`: `request id`

### HTTP Response
* Status Code `200`
* Body `(application/json)`

> Request Object

```json
{
    "status": "Accepted"
}
```

> Response Object

```json
{
    "status": "success",
    "data": [
        {
            "id": 9,
            "rideid": 9,
            "userid": 11,
            "status": "Requested",
            "notification": null
        }
    ]
}
```
