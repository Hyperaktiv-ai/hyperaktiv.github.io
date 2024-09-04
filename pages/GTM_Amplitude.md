---
layout: default
title: GTM to Amplitude
parent: Tracking setup
nav_order: 3
description: "Sending events from Google Tag Manager to Amplitude"
---
{% include variables.md %}
{% raw %}

# Introduction

As you added the previous Javascript snippets to your website / app, we can now capture those events in GTM.

# Triggers
Create 1 trigger for each event that is pushed in GTM's datalayer (select the type ``Custom event``) :
- "Event - signup"
- "Event - login"
- "Event - logout"
- "Event - purchase"
- for each custom event : "Event - my custom event"

You can also create triggers which are not based on datalayer events :
* when a button / link is clicked
* when a page is displayed

Avoid selectors based on the text of a button / link, as this text can change (translations) ; instead, use css / xpath and ids.
Ask for our support on [Slack community] if you struggle setting up triggers.

# Variables
Create 1 variable for each event property set in the events (select the type ``Data Layer variable``) :
- "datalayer - provider"
- "datalayer - user_email"
- "datalayer - user_id"
- "datalayer - amount"
- "datalayer - currency"
- "datalayer - product"
- "datalayer - type"

# Tags

1. Install the Amplitude SDK template : create a new tag > open the Community Template Gallery > find ``Amplitude Analytics Browser SDK``
2. Create a lookup table variable named ``Amplitude - API key``
   * set the API key of the Amplitude project, associated with the hostname of your website
   * leave the default value blank
   * (if you have multiple environments for your website/webapp, we recommend to create a different Amplitude project --> so you can set a different API key associated to the env domain)
3. Create the following tags with type ``Amplitude Analytics Browser SDK`` :
    1. "Amplitude - init" :
        * Tag type : ``Initialize (init)``
        * API Key : ``{{Amplitude - API key}}``
        * Triggering : ``Initialisation - All Pages``
    2. "Amplitude - 'signup'" :
        * Tag type : ``Track Event (track)``
        * Event type : ``signup``
        * Individual Event Properties :
            * Property Name : ``provider``
            * Property Value : ``{{datalayer - provider}}``
        * Triggering : ``Event - signup``
    3. "Amplitude - 'login'" :
        * Tag type : ``Track Event (track)``
        * Event type : ``login``
        * Individual Event Properties :
            * Property Name : ``provider``
            * Property Value : ``{{datalayer - provider}}``
        * Triggering : ``Event - login``
    4. "Amplitude - setUserId" :
        * Tag type : ``Set User ID (setUserId)``
        * User ID : ``{{datalayer - user_id}}``
        * Triggering : ``Event - signup`` and ``Event - login``
    5. "Amplitude - identify" :
        * Tag type : ``Set User Properties (identify)``
        * Operation :
            * Method Call : ``Set``
            * User Property : ``user_email``
            * Value : ``{{datalayer - user_email}}``
        * Triggering : ``Event - signup`` and ``vent - login``
    6. "Amplitude - reset" :
        * Tag type : ``Reset User (reset)``
        * Triggering : ``Event - logout``
    7. "Amplitude - revenue" :
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
    8. "Amplitude - custom events" :
        * Tag type : ``Track Event (track)``
        * Event type : ``{{Event}}``
        * Triggering : ``Event - my custom event`` and all other custom events you created

Everything is now ready.
Just use the "Preview" mode in GTM to check that all events are properly captured by GTM.

# Next

[Integration with Hyperaktiv](/pages/Amplitude_Hyperaktiv)

{% endraw %}

[Slack community]: https://join.slack.com/t/hyperaktivcommunity/shared_invite/zt-2gxxifo1f-N1lKn5~V32Hgvpx4~oi4IA
