---
layout: default
title: User activation
parent: Pushing events to GTM
nav_order: 2
description: "How to track user activation"
---
{% include variables.md %}
{% raw %}

# Introduction

The activation of your users is a very important goal that we want to monitor closely. There should be at least 1 feature in your product that is considered an "activation feature", and there can be several.

# Push activation events to Google Tag Manager
For each feature in your product, add this piece of Javascript :
````
dataLayer.push({
  'event': 'my activation feature'
});
````

Replace "my activation feature" by the right value for your use case.

# Send events from GTM to Amplitude

## Triggers
Create the following triggers with type ``Custom event`` :
- "Event - my activation feature" :
	* Event name : ``my activation feature``

Create as many triggers as you have activation events

## Tags
Create the following tags with type ``Amplitude Analytics Browser SDK`` :
- "Amplitude - 'my activation feature'" :
	* Tag type : ``Track Event (track)``
	* Event type : ``my activation feature``
	* Triggering : ``Event - my activation feature``

If you have multiple triggers, and you want to avoid creating as many tags, you can create only 1 tag associated with all triggers, and define the Event type as : ``{{Event}}``. The exact name of the source custom event will be used.

Everything is now ready.
Just use the "Preview" mode in GTM to check that all events are properly captured by GTM.

# Next step >>

[User conversion](/pages/GTM/Events/Conversion)

{% endraw %}

