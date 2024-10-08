---
layout: default
title: Tracking setup
nav_order: 4
description: "How to implement tracking with Google Tag Manager and Amplitude"
has_children: true
has_toc: false
---
{% include variables.md %}
{% raw %}

# Tracking setup

The tracking infrastructure involves several tools, that have a specific role: 
* [Google Tag Manager] : script injection, centralization of events and publication to 1 or several tracking softwares
* [Amplitude] : 1 of those tracking softwares, collecting the events and taking care of user identification across devices and locations
* [Hyperaktiv] : segmentation of users, hyper-personalization and automation in order to increase your signups and conversions

There are four steps, it takes only a few minutes :
1. [Installation of GTM](/pages/GTM/Install)
2. [Amplitude with GTM](/pages/GTM/Amplitude)
3. [Hyperaktiv with Amplitude](/pages/Hyperaktiv_Amplitude)
4. [Pushing events to GTM](/pages/GTM/Events)

{% endraw %}