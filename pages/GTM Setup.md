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

Read this first : [Setup and install GTM](https://support.google.com/tagmanager/answer/6103696){:target="_blank"}{:rel="noopener noreferrer"}.

It is recommended to create only one web container for both the website and the webapp.
In case of mobile apps, there should be 1 container for iOS, another one for Android.
We might also need a "server" container later, but let's see.

Follow the installation guide for both the website and the webapp.
You can test that the container is deployed properly using the "Preview" in GTM, both on the website and the webapp. The tag assistant should confirm that the container is deployed by displaying the message "Tag Assistant Connected" 
You might need to disable any adblocker in the webbrowser, cause they might block GTM script from being executed.

NB :
- In case of a website built with a CMS, the installation might be a bit different
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
 'event': 'revenue',
 'amount': 15,
 'currency': 'EUR',
 'product': 'basic_plan',
 'type': 'yearly'
 });
````
(Replace the amount, currency, product and type by the correct values)

## Activation event
On every specific action that you consider worth being tracked, add this piece of Javascript :
````
dataLayer.push({
  'event': 'my activation event'
});
````
You can add as many custom event properties as you want.

# Tracking configuration in GTM

As you added the previous javascript snippets to your website / app, we can now capture those events in GTM.

## Triggers
Create 1 trigger for each event that is pushed in GTM's datalayer (select the type "Custom event") :
- "Event - signup"
- "Event - login"
- "Event - logout"
- "Event - revenue"
- "Event - my activation event"

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

1. Install the Amplitude SDK template : create a new tag > open the Community Template Gallery > find "Amplitude Analytics Browser SDK"
2. Create one tag "Amplitude - init" with the 

