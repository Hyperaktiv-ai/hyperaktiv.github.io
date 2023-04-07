---
layout: default
title: SDK
nav_order: 2
description: "How to integrate Kohomai in your app."
---
# Registration of a new joiner

This service allows you to :
- register a new joiner
- assign them a workflow
- get the url of a web page where they can complete their journey
- redirect them to a specific URL once all available activities of the journey are completed

## Retrieve the id of the workflow

You will need the ``id`` of the workflow you want to register new joiners for. Two options :
  * in the back-office, edit the workflow ; the URL is ``https://app.kohomai.com/p/workflows/edit/xxx``, where "xxx" is the ``id`` of the workflow.
  * with the API, find your workflow using [``GET /workflows``](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/workflows/get_workflows) endpoint.

## Registration of a new joiner

### Option 1 : API call

Use [POST /workflows/{workflow-id}/register](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/workflows/post_workflows__workflow_id__register) endpoint.

```json
{
  "RedirectURL": "http://www.google.com",
  "User": {
    "Firstname": "John",
    "Lastname": "Doe",
    "UsrContactPrefs": {
      "PersonalEmail": "johndoe@kohomai.com"
    }
  }
}
```

### Option 2 : Javascript

```js
fetch('https://app.kohomai.com/api/v1/workflows/' + xxx + '/register', {
    method: 'POST',
    headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({ "RedirectURL": "http://www.google.com", "User": { "Firstname": "John", "Lastname": "Doe", "UsrContactPrefs": { "PersonalEmail": "john.doe@gmail.com" } } })
})
   .then(response => response.json())
   .then(response => console.log(JSON.stringify(response)))
```

## Web page to complete the journey

The response contains the URL you have to open for the new joiner to complete their journey :

```json
{
    "UUID": "2bb35288-f2ac-4c68-b7aa-51acd82af485",
    "RedirectURL": "http://www.google.com",
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

# Completion of the journey for an existing new joiner

This service allows you to :
- get the URL of a web page where an existing new joiner can complete their journey
- redirect them to a specific URL once all available activities of the journey are completed

## Retrieve the id of the new joiner

You will need the ``id`` of the new joiner you want to open a session for. Two options :
  * in the back-office, edit the new joiner ; the URL is ``https://app.kohomai.com/p/settings/users/xxx``, where "xxx" is the ``id`` of the new joiner.
  * with the API, find your new joiner using [``GET /users``](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/users/get_users) endpoint.

## Creation of a session

### Option 1 : API call

Use [POST /sessions](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/sessions/post_sessions) endpoint.
```json
{
    "User": {
        "Id" : 74590868830731162
    },
    "RedirectURL": "https://www.google.com"
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
    body: JSON.stringify({ "RedirectURL": "http://www.google.com", "User": { "Id": "xxx" } } })
})
   .then(response => response.json())
   .then(response => console.log(JSON.stringify(response)))
```

## Web page to complete the journey

The response contains the URL you have to open for the new joiner to complete their journey :

```json
{
    "UUID": "2bb35288-f2ac-4c68-b7aa-51acd82af485",
    "RedirectURL": "http://www.google.com",
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
