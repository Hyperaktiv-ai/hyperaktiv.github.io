---
layout: default
title: Hyperaktiv API
nav_order: 6
description: "API"
---
{% include variables.md %}

# Hyperaktiv API

Base url for the API is ``https://app.swaggerhub.com/apis-docs/Hyperaktiv/api``.

Our API documentation is accessible here (Postman) : [api.hyperaktiv.ai](http://api.hyperaktiv.ai/){:target="_blank"}

Swagger is available here : [Swagger](https://app.swaggerhub.com/apis/Hyperaktiv-ai/api){:target="_blank"}

# API authentication

Authentication is implemented through a Bearer token, which is unique and linked to your workspace only.

Your API key can be found in the back-office : "Settings" menu > "API".

Each call to our API require the following header (where ``[YOUR_API_KEY]`` has to be replaced by your API key) :

````
"Authorization": "Bearer [YOUR_API_KEY]"
````

# Import users (deprecated)

1. In the back-office, add an API endpoint as an origin in your funnel ; a reference code is generated.
2. Call [POST /leads]({{ apiUrl }}#/leads/post_leads){:target="_blank"}{:rel="noopener noreferrer"} endpoint.

The reference of the origin has to be set as "ref" parameter. You can find the reference in the back-office by opening the funnel, and clicking on the API origin.

Body :
```json
{
    "Email": "johndoe@gmail.com"
}
```

## Javascript

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

## Can I send more information about my user 

Yes, it's possible to send more information about your user. Details can be found [here]({{ apiUrl }}#/leads/post_leads){:target="_blank"}{:rel="noopener noreferrer"}.

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
