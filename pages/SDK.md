---
layout: default
title: SDK
nav_order: 2
description: "How to integrate Kohomai in your app."
---
# SDK

## Registration of a new joiner

This service allows you to :
- register a new joiner
- assign them a workflow
- get the url of a web page where they can complete their journey
- redirect them to a specific URL once all available activities of the journey are completed

1. You will need the ``id`` of the workflow you want to register new joiners for. Two options :
  * in the back-office, edit the workflow ; the URL is ``https://app.kohomai.com/p/workflows/edit/xxx``, where "xxx" is the ``id`` of the workflow.
  * with the API, find your workflow using [``GET /workflows``](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/workflows/get_workflows) endpoint.
2. Use [POST /workflows/{workflow-id}/register](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/workflows/post_workflows__workflow_id__register) endpoint.

![image](https://user-images.githubusercontent.com/3019346/230613915-302ef1e0-3448-4977-8653-3773ab889452.png)

3. The webservice's response indicates the URL you have to open for the new joiner to complete their journey :

![image](https://user-images.githubusercontent.com/3019346/230613865-96859469-380f-4d83-87e0-9225ae2f16c0.png)

## Complete a journey

This service allows you to :
- get the URL of a web page where an existing new joiner can complete their journey
- redirect them to a specific URL once all available activities of the journey are completed

1. You will need the ``id`` of the new joiner you want to open a session for. Two options :
  * in the back-office, edit the new joiner ; the URL is ``https://app.kohomai.com/p/settings/users/xxx``, where "xxx" is the ``id`` of the new joiner.
  * with the API, find your new joiner using [``GET /users``](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/users/get_users) endpoint.
2. Use [POST /sessions](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0#/sessions/post_sessions) endpoint.

![image](https://user-images.githubusercontent.com/3019346/230616621-269db653-23a6-48f6-9f34-25b8b4c2fa72.png)

3. The webservice's response indicates the URL you have to open for the new joiner to complete their journey :

![image](https://user-images.githubusercontent.com/3019346/230616671-97be7b8a-04a4-4fdb-98c1-6a2b7b960b8d.png)
