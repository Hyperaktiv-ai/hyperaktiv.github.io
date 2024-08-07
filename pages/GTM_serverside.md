---
layout: default
title: Server-side GTM
parent: Tracking setup
nav_order: 2
description: "How to push events to GTM server"
---
{% include variables.md %}

# Introduction
Using server-side tracking (also called server-side tagging) is useful for several reasons :
* avoid ad blockers to block tracking on the client side
* being able to collect events when the web browser cannot be used ; for example : webhooks from payment solutions/ads
The full documentation from Google is [here](https://developers.google.com/tag-platform/tag-manager/server-side/intro).

# How-to

1. First, let's create a server container in GTM. This requires a billing account in GCP ; don't worry about the cost, it will be veery small (less than 1€ a month, unless you have thousands of purchases a day)
2. We recommend to use the GA measurement protocol, which is natively available in GTM server.
3. n your backend, the event can be sent to GTM server container as a POST on ``https://[serverUrl]/g/collect``

The following parameters have to be set in the POST query :
* ``em`` (Event name) : purchase
* ``cid`` (Client Id) : the unique identifier to the client or device ; this has to be consistent with the user id used for the client side tracking, in the web container you're already using
* ``tid`` (Tracking id) : the GA protocol requires this parameter to be set. Let's set a fake value here like "G-123456", even though it doesn't relate to a real measurement in GA.
* ``price`` : the price of the item
* ``quantity`` : the quantity purchased
* ``amount`` : basically price x quantity
* ``currency`` : the currency used (for example "eur")
* ``revenue_type`` : can be used to make a distinction between one-time payments and subscriptions (monthly / yearly)
* ``item_id`` : the id of the purchased item

We recommend to set the following parameters as well:
* ``env`` : can be used to identify the environment, and adjust the propagation of the events in GTM
* ``item_name`` : the name of the purchased item

The complete list of standards parameters can be found [here](https://developers.google.com/analytics/devguides/collection/protocol/ga4/reference/events#purchase). Keep in mind that this list is just a suggestion, as the protocol supports any parameter, and anyways we will have to map each parameter receive to a different name depending on the destination.

4. On the tag configuration screen, the values of the parameters have to be set. Because we use the GA measurement protocol, they can be defined either :
* as "Query parameter" variables
* as "Event data" + mapping to a target property name (depending on the destination requirements). The prefix is "x-ga-mp2-" (ie : the query parameter "currency" becomes "x-ga-mp2-currency"). Be careful, sometimes the mapping doesn't work, I have no idea why (example: "x-ga-mp2-price" was not created by GTM)

Example : 
``https://server-side-tagging-sebsevzwpa-uc.a.run.app/g/collect?v=2&en=purchase&tid=G-12345678&cid=johndoe&amount=100&price=25&quantity=4&currency=eur&revenueType=one-time-payment&productId=book``

5. Create a trigger : custom event "purchase"
6. Create an Amplitude tag with the following mappings :
  - The event should be sent as ``[Amplitude] Revenue``
  - the quantity should be sent as ``$quantity``
  - the product should be sent as ``$productId``
  - the revenue type should be sent as ``$revenueType``
  - the amount should be sent as ``$revenue``
  - the price should be sent as ``$price``
  - the crrency should be sent as ``currency``
  - the ``user_id`` property has to be set as "Additional property key", in order to override the default "device_id" property.

NB : instead of using the GA measurement protocol, it is also possible to use [Stape.io client template](https://github.com/stape-io/data-client/tree/main?tab=readme-ov-file)
