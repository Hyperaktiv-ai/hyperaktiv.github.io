---
layout: default
title: Front-office session
nav_order: 4
description: "Get the URL of the web interface for an existing lead."
---
{% assign apiURL = "https://app.swaggerhub.com/apis-docs/Kohomai/api/1.76.2" %}
{% include _includes/variables.md %}
{{ apiUrl2 }}

# Front-office session

When your funnel contains activities which are assigned to the role "Lead", these activities are automatically made accessible to your leads for completion. You can review the status of each activity in the journey of a specific lead in the back-office (tab "Journey" on a lead's page) or with the API ([``GET /journeys/{journey-id}``]({{ apiURL }}#/journeys/get_journeys__journey_id_){:target="_blank"}{:rel="noopener noreferrer"}).
Leads have to complete their activities using the web interface. They can either login by themselves through the login page, or you can use our API to get a magiclink and redirect them to this URL, where they would be automatically logged in. The magiclink can be used only once.

In order to call this API endpoint, you need to know the journey id of the lead.

## How do I find the journey id of a lead

You have 2 options to find the ``id`` of the journey linked to the lead you want to open a session for :
  * in the back-office, open the page showing the details of the lead : menu "Leads" then select the lead ; the URL is ``https://app.kohomai.com/p/journeys/xxx``, where "xxx" is the ``id`` of the journey.
  * with an API client (like Swagger or Postman for example), find the journey using [``GET /journeys``]({{ apiURL }}#/journeys/get_journeys){:target="_blank"}{:rel="noopener noreferrer"} endpoint.

## Open a session and get Magic Link

The "RedirectURL" attribute is optional ; you can use it in order to automatically redirect the lead once all they completed all available activities.

### Option 1 : API call

Use [POST /sessions]({{ apiURL }}#/sessions/post_sessions){:target="_blank"}{:rel="noopener noreferrer"} endpoint.
```json
{
    "Journey": {
        "Id" : xxx
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
        'Content-Type': 'application/json',
        'Authorization': 'Bearer XXX'
    },
    body: JSON.stringify({ "Journey": { "Id": "xxx" }, "RedirectURL": "https://www.myapp.com" } })
})
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
