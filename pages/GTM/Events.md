---
layout: default
title: 4. Pushing events to GTM
parent: Tracking setup
nav_order: 4
description: "How to push events to Google Tag Manager"
has_children: true
has_toc: false
---
{% include variables.md %}
{% raw %}

# Pushing events from the website / app to GTM

To send events to Google Tag Manager, we use a javascript object called ``dataLayer`` (automatically available as soon as Google Tag Manager's scripts are loaded).
Inside your app, you will need to insert some short javascript code to send specific events to GTM. Don't worry if you're not a software developer, it's very simple, and we're here to support you. Just ping us on [Slack community].

The typical code looks like this :
````
dataLayer.push({
  'event': 'my event',
  'property 1': 'value 1',
  'property 2': 'value 2'
});
````

We do recommend to always write event names in lower case, and to avoid special characters.

# Sending events from GTM to Amplitude

In Google Tag Manager, you will have to create :
* 1 Trigger with type ``Custom event`` for each event pushed in the dataLayer
* 1 Variable with type ``Data Layer variable`` for each property pushed with any event
* 1 Tag for each tracking software you want to send an event to

The same trigger can be associated with multiple tags --> several tracking softwares will receive the same event

# Implementation

We recommend to track key events in your user's lifecycle :
* User identification
* User activation
* User conversion

It might also be interesting to track :
* When a user starts a trial
* Some other custom events

# Next step >>

[User identification](/pages/GTM/Events/Identification)

{% endraw %}

