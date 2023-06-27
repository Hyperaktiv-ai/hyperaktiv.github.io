---
layout: default
title: Lead registration
nav_order: 3
description: "How to register a new lead in Kohomai"
---

# How to register a new lead in Kohomai

Leads can be added to Kohomai using 3 different ways :
- manually using the back-office (menu "Leads", then "New" button)
- programmatically using the API
- leads can register themselves autonomously through a registration page
When a lead is registered, and a funnel is assigned to them, their journey is automatically generated.

In order to call this API endpoint, you need to know the id of the funnel you want to assign the lead to.

## How do I find the id of a funnel

You have 2 options to find the ``id`` of the funnel you want to register leads on :
  * in the back-office, edit the funnel ; the URL is ``https://app.kohomai.com/p/funnels/edit/xxx``, where "xxx" is the ``id`` of the funnel.
  * with an API client (like Swagger or Postman for example), find your funnel using [``GET /funnels``](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/funnels/get_funnels){:target="_blank"}{:rel="noopener noreferrer"} endpoint.

## Registration of a new lead

The "RedirectURL" attribute is optional ; you can use it in order to automatically redirect the lead once all they completed all available activities.
The "JourneyData" attribute is optional ; you can use it in order to add data to the generated journey (the data points have to be created prior in your workspace).

### Option 1 : API call

1. In the back-office, add an API endpoint as a starting point in your funnel ; a reference code is generated.
2. Call [POST /journeys](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/journeys/post_journeys){:target="_blank"}{:rel="noopener noreferrer"} endpoint.

Parameter : "ref=[the generated reference code of the starting point]"
Body :
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
fetch('https://app.kohomai.com/api/v1/journeys?ref=YYY', {
    method: 'POST',
    headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json',
        'Authorization': 'Bearer XXX'
    },
    body: JSON.stringify({
    "Journey": { "User": { "Firstname": "John", "Lastname": "Doe", "ContactPrefs": { "Email": "johndoe@gmail.com" }}}, "RedirectURL": "https://www.myapp.com"
    }) })
   .then(response => response.json())
   .then(response => console.log(JSON.stringify(response)))
```

### URL of the web front-office to complete the journey

The response contains the URL you have to open for the lead to complete their journey (attribute "ConnectionURL") :

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
