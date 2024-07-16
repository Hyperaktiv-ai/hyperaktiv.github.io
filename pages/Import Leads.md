---
layout: default
title: Import Leads
nav_order: 3
description: "How to import leads into Hyperaktiv"
---
{% include variables.md %}

# How to import a new lead in Hyperaktiv

Leads can be imported into Hyperaktiv using 4 different ways :
- automatically from Amplitude
- through the API
- manually using the back-office
- automatically from HubSpot

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
fetch('https://app.hyperaktiv.ai/api/v1/leads?ref=YYY', {
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
