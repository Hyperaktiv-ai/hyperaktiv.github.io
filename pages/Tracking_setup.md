---
layout: default
title: Tracking setup
nav_order: 4
description: "How to implement tracking with Google Tag Manager and Amplitude"
has_children: true
---
{% include variables.md %}
{% raw %}


The tracking infrastructure involves several tools, that have a specific role: 
* [Google Tag Manager] : script injection, centralization of events and publication to 1 or several tracking softwares
* [Amplitude] : 1 of those tracking softwares, collecting the events and taking care of user identification across devices and locations
* [Hyperaktiv] : segmentation of users and hyper-personalization automation in order to increase your conversions

There are four steps, it takes only a few minutes :
1. [Hyperkativ with Amplitude](/pages/Hyperaktiv_Amplitude)
2. [Installation of Google Tag Manager](/pages/GTM/Install)
3. [Amplitude with GTM](/pages/GTM/Amplitude)
4. [Pushing events to GTM](/pages/GTM/Events)

{% endraw %}
