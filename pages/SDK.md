---
layout: default
title: SDK
nav_order: 2
description: "How to integrate Kohomai in your app."
---
# Registration of an end user

This service allows you to :
- register an end user and start their journey
- get the url of a web page where they can complete their journey
- redirect them to a specific URL once all available activities of the journey are completed

## Retrieve the id of the workflow

You will need the ``id`` of the workflow you want to register end users for. Two options :
  * in the back-office, edit the workflow ; the URL is ``https://app.kohomai.com/p/funnels/edit/xxx``, where "xxx" is the ``id`` of the workflow.
  * with the API, find your workflow using [``GET /workflows``](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/workflows/get_workflows) endpoint.

## Registration of an end user, and initialization of their journey

### Option 1 : API call

Add an API endpoint as a starting point in your workflow, and use the generatd key to call [POST /journeys](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/journeys/post_journeys) endpoint.

```json
{
    "Journey": {
        "User": {
            "Firstname": "John",
            "Lastname": "Doe",
            "ContactPrefs": {
                "Email": "johndoe@gmail.com"
            }
        },
        "JourneyData" :[
            {
                "StringValue": "example",
                "DataPoint": {
                    "Id": 123456789
                }
            }
        ]
    },
    "RedirectURL": "https://www.myapp.com"
}
```

### Option 2 : Javascript

```js
fetch('https://app.kohomai.com/api/v1/journeys', {
    method: 'POST',
    headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({
    "RedirectURL": "https://www.myapp.com", "Journey": { "User": { "Firstname": "John", "Lastname": "Doe", "ContactPrefs": { "Email": "johndoe@gmail.com" }}}}) })
   .then(response => response.json())
   .then(response => console.log(JSON.stringify(response)))
```

## Web page to complete the journey

The response contains the URL you have to open for the end user to complete their journey :

```json
{
    "UUID": "2bb35288-f2ac-4c68-b7aa-51acd82af485",
    "RedirectURL": "https://www.myapp.com",
    "ConnectionURL": "http://app.kohomai.com/internal/v1/autologin?UUID=2bb35288-f2ac-4c68-b7aa-51acd82af485",
    "ValidUntil": "2022-04-07T13:10:01.614Z",
    "changedDate": "2022-04-07T13:05:01.620Z",
    "createdDate": "2022-04-07T13:04:59.755Z",
    "User": {
        "Firstname": "John",
        "Lastname": "Doe",
        "Id": 74590868830731162
    }
}
```

# Completion of the journey for an existing end user

This service allows you to :
- get the URL of a web page where an existing end user can complete their journey
- redirect them to a specific URL once all available activities of the journey are completed

## Retrieve the id of the end user

You will need the ``id`` of the end user you want to open a session for. Two options :
  * in the back-office, edit the end user ; the URL is ``https://app.kohomai.com/p/settings/users/xxx``, where "xxx" is the ``id`` of the new joiner.
  * with the API, find your end user using [``GET /users``](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/users/get_users) endpoint.

## Creation of a session

### Option 1 : API call

Use [POST /sessions](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/sessions/post_sessions) endpoint.
```json
{
    "User": {
        "Id" : 74590868830731162
    },
    "RedirectURL": "https://www.myapp.com"
}
```

### Option 2 : Javascript

```js
fetch('https://app.kohomai.com/api/v1/sessions', {
    method: 'POST',
    headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({ "RedirectURL": "https://www.myapp.com", "User": { "Id": "xxx" } } })
})
   .then(response => response.json())
   .then(response => console.log(JSON.stringify(response)))
```

## Web page to complete the journey

The response contains the URL you have to open for the end user to complete their journey :

```json
{
    "UUID": "2bb35288-f2ac-4c68-b7aa-51acd82af485",
    "RedirectURL": "https://www.myapp.com",
    "ConnectionURL": "http://app.kohomai.com/internal/v1/autologin?UUID=2bb35288-f2ac-4c68-b7aa-51acd82af485",
    "ValidUntil": "2022-04-07T13:10:01.614Z",
    "changedDate": "2022-04-07T13:05:01.620Z",
    "createdDate": "2022-04-07T13:04:59.755Z",
    "User": {
        "Firstname": "John",
        "Lastname": "Doe",
        "Id": 74590868830731162
    }
}
```
