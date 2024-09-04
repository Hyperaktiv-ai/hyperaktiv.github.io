---
layout: default
title: Tracking principles
nav_order: 2
description: "How to track your users' behavior"
---
{% include variables.md %}

# Tracking principles

A strong tracking infrastructure implemented on your website and app will allow you to better understand your users' behavior.
Here are some of the main questions people have when it comes to user tracking :
* how can we unify data from the website ?
* which tools to use ? how to integrate them ?
* what about consent mode ? ad blockers ? data protection / gdpr ?
* do i need to code ?
* how much time would it take ?

Good news : Hyperaktiv has a simple answer to all those questions.
Spoiler alert : you don't need to know how to code ; and the whole thing should not take more than a few minutes.

Here you will find explanations.
If you want to directly jump to the step-by-step installation, it's [here](/pages/Tracking_setup.html)

# What should I do ?

There are a few great tools on the market today. But unfortunately, not one of them can cover all your needs.
Let's start here : let's dissociate "how/what to track ?" from "which tools should I use ?"

## How/what to track ?
On your website / webapp / mobile app, every time a user is performing an action (opening a page, clicking on a button ...), an event will be recorded. This event contains properties (timestamp, identification of the user, information about their device / web browser, language, location etc). These events should be independant to any tracking software ; we will just send them.

We **do not recommend** to insert the code of tracking softwares directly in your website / webapp. Instead, you should use [Google Tag Manager].

### Google Tag Manager

[Google Tag Manager] is not a tracking software ; its role is to dynamically inject code snippets inside your website / webapp ; those snippets are meant to collect events for tracking softwares.

Why we recommend to use [Google Tag Manager] :
* Flexibility and speed : GTM offers a web console where you can dynamically add / remove tracking codes without touching the code ; the deployment takes 1s, and there is no impact on your code
* Consent mode : GTM offers a simple way to handle the consent mode for your visitors / users
* SEO : the pages load faster cause GTM injects the scripts asynchronously
* Maintenability : when a tracking software publishes a new version of their SDK, GTM notifies you, and you just need to update the template in the webconsole
* Historization : all changes made are logged in GTM, so you can see who changed what and when, and if necessary rollback the configuration
* No hassle : GTM is free, their SDK is extremely stable, and it doesn't retain data (no GDPR related issue)

## Which tools should I use ?

You can find more information about tracking software [here](/pages/Tracking_softwares)

Setting up with [Google Tag Manager] requires only a few minutes ; [let's start](/pages/Tracking_setup).

