---
layout: default
title: Custom events
parent: 4. Pushing events to GTM
grand_parent: Tracking setup
nav_order: 5
description: "How to track custom events"
---
{% include variables.md %}
{% raw %}

# Custom events

## Push event to Google Tag Manager
On every specific action that you consider worth being tracked, add this piece of Javascript :
````
dataLayer.push({
  'event': 'my custom event'
});
````
You can also add event properties if you want.

## Send event from GTM to Amplitude

### Triggers
Create 1 trigger per event with type ``Custom event`` :
- "Event - my custom event" :
	* Event name : ``my custom event``

Create as many triggers as you have activation events.

### Tags
Create 1 tag with type ``Amplitude Analytics Browser SDK`` :
- "Amplitude - Custom events" :
	* Tag type : ``Track Event (track)``
	* Event type : ``{{Event}}``
	* Triggering : ``Event - my custom event`` and all other custom event triggers

Everything is now ready.
Just use the "Preview" mode in GTM to check that all events are properly captured by GTM.

{% endraw %}
