---
layout: default
title: User conversion
parent: Pushing events to GTM
nav_order: 3
description: "How to track revenue / user conversions"
---
{% include variables.md %}
{% raw %}

# User conversion

Revenue tracking might be the most complex configuration to implement, but it is also the most important one.
A ``revenue`` event must be pushed everytime a payment is confirmed by the payment gateway.
Most payment gateways (such as Stripe) offer the possibility to define a callback URL when payment is confirmed ; the revenue event should be pushed when this confirmation is received.
Depending on how your app is structured, there are 2 possibilities :
1. the user is redirected to a confirmation page where the payment information is available or your webapp is Reactive / you have access to the confirmation info in the frontend (client side implementation)
2. the payment information is not available in the frontend (server side implementation)

Don't hesitate to contact us on [Slack community] if you struggle with the implementation.

# Client-side implementation
If the callback URL redirects to a confirmation page displayed to the user, the revenue event can be pushed to GTM's datalayer. The page requires the amount, currency, product and subscription type in order to set the properties, so it might happen that you will have to append those parameters to the callback URL you provide to Stripe, so they can then be extracted in the confirmation page.

If you're using a Reactive webapp, you can push a notification from the backend to the frontend. In this notification, you can add the required parameters and then push the event in GTM's datalayer.

## Push revenue events to Google Tag Manager
Insert this piece of Javascript once the purchased is confirmed :
````
dataLayer.push({
 'event': 'revenue',
 'amount': 15,
 'currency': 'EUR',
 'product': 'basic_plan',
 'type': 'yearly'
 });
````
Replace the amount, currency, product and type by the correct values :
* ``product`` : the name of the product the user purchased, for example : ``basic_plan``, ``enterprise_plan``...
* ``type`` : the type of purchase, for example : ``monthly``, ``yearly``, ``one-time``, ``life-time``...
* ``currency`` : we recommend to use a standard 3 letter-long code ; for example ``EUR``

## Send events from GTM to Amplitude

## Triggers
Create the following triggers with type ``Custom event`` :
- "Event - revenue" :
	* Event name : ``revenue``

## Variables
Create the following variables with type ``Data Layer Variable`` :
- "datalayer - amount"
	* Data Layer Variable Name : ``amount``
- "datalayer - currency"
	* Data Layer Variable Name : ``currency``
- "datalayer - product"
	* Data Layer Variable Name : ``product``
- "datalayer - type"
	* Data Layer Variable Name : ``type``

## Tags
Create the following tags with type ``Amplitude Analytics Browser SDK`` :
- "Amplitude - revenue" :
	* Tag type : ``Track Revenue (revenue)``
	* Product ID : ``{{datalayer - product}}``
	* Product Price : ``{{datalayer - amount}}``
	* Product Quantity : ``1``
	* Revenue : ``{{datalayer - amount}}``
	* Revenue Type : ``{{datalayer - type}}``
	* Event Properties :
		* Property Name : ``currency``
		* Property Value : ``{{datalayer - currency}}``
	* Triggering : ``Event - revenue``

# Server-side implementation
If the payment confirmation is not available in the frontend, then GTM's datalayer is not available. In that situation, there are several options to push the revenue event to tracking softwares:
1. Using [Amplitude] API
2. Using a Server GTM container
3. Pushing through Segment (or any other ETL)

## 1. Using Amplitude API

With this approach, you will have to write 1 API call for each destination. Here we will explicit only [Amplitude], but it will be the same logic for [Mixpanel], [Google Analytics] etc.

API call details:
* Method : ``POST``
* Server : ``https://api.amplitude.com/2/httpapi`` (US projects) or ``https://api.eu.amplitude.com/2/httpapi`` (EU projects)
* Headers : ``Content-Type: application/json``

````
{
  "api_key": "{{api_key}}",
  "events": [
    {
      "user_id": "{{user_id}}",
      "event_type": "revenue",
      "event_properties": {
        "currency": "{{currency}}"
      },
      "price": {{amount}},
      "quantity": 1,
      "revenue": {{amount}},
      "productId": "{{productId}}",
      "revenueType": "{{type}}"
    }
  ]
}
````
Just replace the parameters in ``{{..}}`` with the right values.

Here is the [full documentation](https://amplitude.com/docs/apis/analytics/http-v2#request)

## 2. Server GTM container
This approach (also called server-side tagging) consists in creating a new "Server" container in Google Tag Manager, and from there pushing the event to [Amplitude] and other destinations. The main downside of this approach is that the container is a virtual machine on Google Cloud Platform, which requires a billing account. The VM would be in the free tier for some time, but depending on the volume of events, you could be charged. If we stick to revenue events only, then it's a very small cost (<1€ a month if less than 100 revenue events a month).
--> we do not recommend to use the server-side tracking when it's possible to use the client-side (free).


1. First, let's create a server container in GTM. This requires a billing account in GCP.
2. We recommend to use the GA measurement protocol, which is natively available in GTM server.
3. In your backend, the event can be sent to GTM server container as a ``POST`` on ``https://[serverUrl]/g/collect``

The following parameters have to be set in the ``POST`` query :
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

5. Create a trigger with type ``custom event`` : "purchase"
6. Create a tag with type ``Amplitude`` :
  - event name : ``revenue_amount`` (this is the default name, but you can choose another one)
  - the quantity should be sent as ``$quantity``
  - the product should be sent as ``$productId``
  - the revenue type should be sent as ``$revenueType``
  - the amount should be sent as ``$revenue``
  - the price should be sent as ``$price``
  - the crrency should be sent as ``currency``
  - the ``user_id`` property has to be set as "Additional property key", in order to override the default "device_id" property.

NB : instead of using the GA measurement protocol, it is also possible to use [Stape.io client template](https://github.com/stape-io/data-client/tree/main?tab=readme-ov-file)


## 3. Using Segment or another ETL
Just push the event to Segment / your ETL using the SDK that fits your tech stack (this part requires some coding skills). Then in the web console of your ETL, push the event to [Amplitude] (this should not require to code). The exact implementation depends on your ETL.

[How to push events to Segment with the API](https://segment.com/docs/connections/sources/catalog/libraries/server/http-api/#track)

# Next step >>

[User trial](/pages/GTM/Events/Trial)

{% endraw %}
