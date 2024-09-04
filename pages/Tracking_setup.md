---
layout: default
title: Tracking setup
nav_order: 4
description: "How to implement your tracking infrastructure"
has_children: true
---
{% include variables.md %}
{% raw %}

# Introduction

The tracking infrastructure involves several tools, that have a specific role: 
* Google Tag Manager : script injection, centralization of events and publication to 1 or several tracking softwares
* Amplitude : 1 of those tracking softwares, collecting the events and taking care of user identification across devices and locations
* Hyperaktiv : segmentation of users and hyper-personalization automation in order to increase your conversions

There are four steps, it takes only a few minutes :
1. [Installation of Google Tag Manager on your website and webapp](/pages/GTM_install)
2. [Sending events from your website / webapp to GTM](/pages/GTM_events)
3. [Sending events from GTM to Amplitude](/pages/GTM_Amplitude)
4. [Integration between Amplitude and Hyperaktiv](/pages/Amplitude_Hyperaktiv)

{% endraw %}

[Slack community]: https://join.slack.com/t/hyperaktivcommunity/shared_invite/zt-2gxxifo1f-N1lKn5~V32Hgvpx4~oi4IA
