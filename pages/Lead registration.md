---
layout: default
title: Lead registration
nav_order: 3
description: "How to register a new lead in Kohomai"
---
{% include variables.md %}

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
  * with an API client (like Swagger or Postman for example), find your funnel using [``GET /funnels``]({{ apiUrl }}#/funnels/get_funnels){:target="_blank"}{:rel="noopener noreferrer"} endpoint.

## Registration of a new lead

The "JourneyData" attribute is optional ; you can use it in order to add data to the generated journey (the data points have to be created prior in your workspace).
The "WebhookInput" attribute is optional ; you can use it in order to receive notification when specific events related to this lead occur.

### Option 1 : API call

1. In the back-office, add an API endpoint as an origin in your funnel ; a reference code is generated.
2. Call [POST /leads]({{ apiUrl }}#/leads/post_leads){:target="_blank"}{:rel="noopener noreferrer"} endpoint.

The reference of the origin has to be set as "ref" parameter. You can find the reference in the back-office by opening the funnel, and clicking on the API origin.

Body :
```json
{
    "Email": "johndoe@gmail.com"
}
```

### Option 2 : Javascript

```js
fetch('https://app.kohomai.com/api/v1/leads?ref=YYY', {
    method: 'POST',
    headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json',
        'Authorization': 'Bearer XXX'
    },
    body: JSON.stringify({ "Email": "johndoe@gmail.com" }) })
   .then(response => response.json())
   .then(response => console.log(JSON.stringify(response)))
```

### Can I send more information about my lead 

Yes, it's possible to send more information about your lead. Details can be found [here]({{ apiUrl }}#/leads/post_leads){:target="_blank"}{:rel="noopener noreferrer"}.

Body :
```json
{
    "Email": "johndoe@gmail.com",
    "Firstname": "John",
    "Lastname": "Doe",
    "PhoneNumber": "+1 (800) 555‑0175",
    "RedirectURL": "https://www.myapp.com",
    "JourneyData" :[
        {
            "Name": "My datapoint",
            "Value": "example"
        }
    ]
}
```
