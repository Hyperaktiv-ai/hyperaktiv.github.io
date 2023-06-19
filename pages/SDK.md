---
layout: default
title: SDK
nav_order: 2
description: "How to integrate Kohomai in your app."
---
# Registration of a lead

This service allows you to :
- register a lead and start their journey
- get the url of the front-office where they can complete their journey (if you want them to) 
- redirect them to a specific URL once they completed all available activities

## Retrieve the id of the funnel

You will need the ``id`` of the funnel you want to register leads on. Two options :
  * in the back-office, edit the funnel ; the URL is ``https://app.kohomai.com/p/funnels/edit/xxx``, where "xxx" is the ``id`` of the funnel.
  * with the API, find your funnel using [``GET /workflows``](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/funnels/get_funnels) endpoint.

## Registration of a lead, and initialization of their journey

### Option 1 : API call

Add an API endpoint as a starting point in your funnel, and use the generated reference to call [POST /journeys](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/journeys/post_journeys) endpoint.

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
    "Journey": { "User": { "Firstname": "John", "Lastname": "Doe", "ContactPrefs": { "Email": "johndoe@gmail.com" }}}, "RedirectURL": "https://www.myapp.com"
    }) })
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

# Completion of the journey for an existing lead

This service allows you to :
- get the url of the front-office where they can complete their journey (if you want them to) 
- redirect them to a specific URL once they completed all available activities

## Retrieve the id of the lead

You will need the ``id`` of the lead you want to open a session for. Two options :
  * in the back-office, open the page showing the details of the lead : Menu "Leads" > click on one lead, then click on the "edit" button on the top right of the screen ; the URL is ``https://app.kohomai.com/p/settings/users/xxx``, where "xxx" is the ``id`` of the lead.
  * with the API, find your lead using [``GET /users``](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/users/get_users) endpoint.

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

The response contains the URL you have to open for the lead to complete their journey :

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
