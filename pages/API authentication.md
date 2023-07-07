---
layout: default
title: API authentication
nav_order: 2
description: "API authentication"
---

# API authentication

Authentication is implemented through a Bearer token, which is unique and linked to your workspace only.

## Where can I find my API key ?

Your API key can be found in the back-office : "Settings" menu > "API".

## How to use my API key ?

Each call to our API require the following header (where ``[YOUR_API_KEY_HERE]`` has to be replaced by your API key) :

````
"Authorization": "Bearer [YOUR_API_KEY_HERE]"
````
