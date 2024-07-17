---
layout: default
title: GTM Setup
nav_order: 3
description: "Google Tag Manager setup"
---
{% include variables.md %}

# Introduction

Three steps :
1. Installation of Google Tag Manager
2. Event tracking configuration in GTM
3. Integration with Hyperaktiv

# Installation of Google Tag Manager

Read this : [Setup and install GTM](https://support.google.com/tagmanager/answer/6103696){:target="_blank"}{:rel="noopener noreferrer"}.

It is recommended to create only one web container for both the website and the webapp.
In case of mobile apps, there should be 1 container for iOS, another one for Android.
We might also need a "server" container later, but let's see.

Follow the installation guide for both the website and the webapp.
You can test that the container is deployed properly using the "Preview" in GTM, both on the website and the webapp. The tag assistant should confirm that the container is deployed by displaying the message "Tag Assistant Connected" 
You might need to disable any adblocker in the webbrowser, cause they might block GTM script from being executed.

NB :
- In case of a website built with a CMS, the installation might be a bit different ; use the Preview to ensure that the container is well deployed
- In case there is already some hard-coded tags implemented, we recommend to migrate the existing tags to [Google Tag Manager], and then remove the old hard-coded tracking tags.

# Sending events from the website / app to GTM

Inside your app, you will need to insert some code to send specific events to GTM.

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

## Purchase
When your user finalized a subscription / purchase, add this piece of Javascript :
````
dataLayer.push({
 'event': 'purchase',
 'amount': 15,
 'currency': 'EUR',
 'product': 'basic_plan',
 'type': 'yearly'
 });
````
(Replace the amount, currency, product and type by the correct values)

## Custom event
On every specific action that you consider worth being tracked, add this piece of Javascript :
````
dataLayer.push({
  'event': 'my custom event'
});
````
You can also add event properties if you want.

# Tracking configuration in GTM

As you added the previous javascript snippets to your website / app, we can now capture those events in GTM.

## Triggers
Create 1 trigger for each event that is pushed in GTM's datalayer (select the type "Custom event") :
- "Event - signup"
- "Event - login"
- "Event - logout"
- "Event - purchase"
- for each custom event : "Event - my custom event"

You can also create triggers which are not based on datalayer events :
* when a button / link is clicked
* when a page is displayed

Avoid selectors based on the text of a button / link, as this text can change (translations) ; instead, use css / xpath and ids.
Ask for our support on Slack community if you struggle setting up triggers.

## Variables
Create 1 variable for each event property set in the events (select the type "Data Layer variable") :
- "datalayer - provider"
- "datalayer - user_email"
- "datalayer - user_id"
- "datalayer - amount"
- "datalayer - currency"
- "datalayer - product"
- "datalayer - type"

# Integration with Hyperaktiv

1. Create your Amplitude project : 
  * [US based](https://app.amplitude.com/signup)
  * [EU based](https://app.eu.amplitude.com/signup)
2. Copy the API key, or leave the page open
3. In GTM, install the Amplitude SDK template : create a new tag > open the Community Template Gallery > find "Amplitude Analytics Browser SDK"
4. Create a lookup table variable named "Amplitude - API key"
  * set the API key of the Amplitude project, associated with the hostname of your website
  * leave the default value blank
  * (if you have multiple environments for your website/webapp, we recommend to create a different Amplitude project --> so you can set a different API key associated to the env domain)
5. Create the following Amplitude tags :
* "Amplitude - init" :
  * Tag type : ``Initialize (init)``
  * API Key : ``{{{{Amplitude - API key}}``
  * Triggering : ``Initialisation - All Pages``
* "Amplitude - signup" :
  * Tag type : ``Track Event (track)``
  * Event type : ``signup``
  * Individual Event Properties :
    * Property Name : ``provider``
    * Property Value : ``{{datalayer - provider}}``
  * Triggering : ``Event - signup``
* "Amplitude - login" :
  * Tag type : ``Track Event (track)``
  * Event type : ``login``
  * Individual Event Properties :
  ** Property Name : ``provider``
  ** Property Value : ``{{datalayer - provider}}``
  * Triggering : ``Event - login``
* "Amplitude - setUserId" :
  * Tag type : ``Set User ID (setUserId)``
  * User ID : ``{{datalayer - user_id}}``
  * Triggering : ``Event - signup`` and ``Event - login``
* "Amplitude - identify" :
  * Tag type : ``Set User Properties (identify)``
  * Operation :
    * Method Call : ``Set``
    * User Property : ``user_email``
    * Value : ``{{datalayer - user_email}}``
  * Triggering : ``Event - signup`` and ``vent - login``
* "Amplitude - setUserId" :
  * Tag type : ``Reset User (reset)``
  * Triggering : ``Event - logout``
* "Amplitude - revenue" :
  * Tag type : ``Track Revenue (revenue)``
  * Product ID : ``{{datalayer - product}}``
  * Product Price : ``{{datalayer - amount}}``
  * Product Quantity : ``1``
  * Revenue : ``{{datalayer - amount}}``
  * Revenue Type : ``{{datalayer - type}}``
  * Event Properties :
    * Property Name : ``currency``
    * Property Value : ``{{datalayer - currency}}``
  * Triggering : ``Event - purchase``
* "Amplitude - custom events" :
  * Tag type : ``Track Event (track)``
  * Event type : ``{{Event}}``
  * Triggering : ``Event - my custom event`` and all other custom events you created
