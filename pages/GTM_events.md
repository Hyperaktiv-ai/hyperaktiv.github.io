---
layout: default
title: Pushing events to GTM
parent: Tracking setup
nav_order: 2
description: "How to push events to GTM"
has_children: true
---
{% include variables.md %}
{% raw %}

# Sending events from the website / app to GTM

To send events to Google Tag Manager, we use a javascript object called ``dataLayer`` (automatically available as soon as Google Tag Manager's scripts are loaded).
Inside your app, you will need to insert some short javascript code to send specific events to GTM. Don't worry if you're not a software developer, it's very simple, and we're here to support you. Just ping us on [Slack community].

## Signup
After a successful signup, add this piece of Javascript :
````
dataLayer.push({
  'event': 'signup',
  'provider': 'email',
  'user_email': 'johndoe@gmail.com',
  'user_id': '123456789'
});
````

(Replace "email" by "google" or any other SSO provider, "user_email" by the email of the user and "user_id" by the internal identifier of a user inside your product)

## Login
After a successful login, add this piece of Javascript :
````
dataLayer.push({
  'event': 'login',
  'provider': 'email',
  'user_email': 'johndoe@gmail.com',
  'user_id': '123456789'
});
````

## Logout
When your user logs out, add this piece of Javascript :
````
dataLayer.push({
  'event': 'logout'
});
````

## Trial started
When your user started a trial, add this piece of Javascript :
````
dataLayer.push({
 'event': 'trial'
 });
````

## Revenue

A ``revenue`` event must be pushed everytime a payment is confirmed by the payment gateway.
Most payment gateways (such as Stripe) offer the possibility to define a callback URL when payment is confirmed ; the revenue event should be pushed when this confirmation is received.
Depending on how your app is structured, there are 2 possibilities :
1. the user is redirected to a confirmation page where the payment information is available (client side implementation)
2. the payment information is not available in a page (server side implementation)

Don't hesitate to contact us on [Slack community] if you struggle with the implementation.

### Client-side implementation
If the callback URL redirects to a confirmation page displayed to the user, the revenue event can be pushed to GTM's datalayer. The page requires the amount, currency, product and subscription type in order to set the properties, so it might happen that you will have to append those parameters to the callback URL you provide to Stripe, so they can then be extracted in the confirmation page.

Insert this piece of Javascript will send an event to Google Tag Manager :
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

### Server-side implementation
If the payment confirmation is not available in the frontend, then GTM's datalayer is not available. In that situation, there are several options to push the revenue event :
1. Directly to Hyperaktiv via [Amplitude] API
2. Sending a notification to the frontend from the backend (reactive apps)
3. Using a Server GTM container
4. Pushing through Segment (or any other ETL)

#### 1. Direct Amplitude API
Here is the [full documentation](https://amplitude.com/docs/apis/analytics/http-v2#request)

Here is a shorter version :
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

#### 2. Backend to frontend notification
Especially if you're using a reactive webapp, you can push a notification from the backend to the frontend, for example to display a confirmation message. In this notification, you can add the required parameters to then, from the frontend, push the event in GTM's datalayer : 
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

#### 3. Server GTM container
This approach consists on creating a new "Server" container in Google Tag Manager, and from there pushing the event to Amplitude. The main downside of this approach is that the container is a VM on GCP, which requires a billing account. The VM would be in the free tier for some time, but depending on the volume of events, you could be charged.
If we stick to revenue events only, then it's a very small cost (<1€ a month if less than 100 revenue events a month).
--> we do not recommend to use the server-side tracking when it's possible to use the client-side (free).
The complete procedure to install is [here](/pages/GTM_serverside)

#### 4. Using Segment or another ETL
Just push the event to Segment / your ETL, and from there, push the event to Amplitude (this should not require to code). The exact implementation depends on your ETL.
[How to push events to Segment with the API](https://segment.com/docs/connections/sources/catalog/libraries/server/http-api/#track)

## Custom event
On every specific action that you consider worth being tracked, add this piece of Javascript :
````
dataLayer.push({
  'event': 'my custom event'
});
````
You can also add event properties if you want.

{% endraw %}

[Slack community]: https://join.slack.com/t/hyperaktivcommunity/shared_invite/zt-2gxxifo1f-N1lKn5~V32Hgvpx4~oi4IA
