---
layout: default
title: User trial
parent: 4. Pushing events to GTM
nav_order: 4
description: "How to track user trials"
---
{% include variables.md %}
{% raw %}

# User trial

Most B2B SaaS business offer a trial to their users. In that case, Hyperaktiv offers the possibility to monitor key metrics related to trials (signup to trial average time, trial rate, trial to conversion rate, etc)

# Push event to Google Tag Manager
When your user started a trial, add this piece of Javascript :
````
dataLayer.push({
 'event': 'trial'
 });
````

# Send event from GTM to Amplitude

## Triggers
Create the following triggers with type ``Custom event`` :
- "Event - trial" :
	* Event name : ``trial``

Create as many triggers as you have activation events

## Tags
Create the following tags with type ``Amplitude Analytics Browser SDK`` :
- "Amplitude - 'trial'" :
	* Tag type : ``Track Event (track)``
	* Event type : ``trial``
	* Triggering : ``Event - trial``

# Next step >>

[Custom events](/pages/GTM/Events/Custom)

{% endraw %}

