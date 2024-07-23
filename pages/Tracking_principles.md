---
layout: default
title: Tracking principles
nav_order: 2
description: "How to track your leads's behavior"
---
{% include variables.md %}

# Introduction

A strong tracking infrastructure implemented on your website and app will allow you to better understand your leads' behavior.
Here are some of the main questions people have when it comes to lead tracking :
* how can we unify data from the website ?
* which tools to use ? how to integrate them ?
* what about consent mode ? ad blockers ? data protection / gdpr ?
* do i need to code ?
* how much time would it take ?

Good news : Hyperaktiv has a simple answer to all those questions.
Spoiler alert : you don't need to know how to code ; and the whole thing should not take more than a few minutes.

Here you will find explanations.
If you want to directly jump to the step-by-step installation, it's [here](/pages/Tracking_setup.html)

# Which tools ?

There are a few great tools on the market today. But unfortunately, not one of them can cover all your needs.
Let's start here : let's dissociate "how/what to track" from "what to do with the data"

## How/what to track
On your website / webapp / mobile app, every time a lead is performing an action (opening a page, clicking on a button ...), an event will be recorded. This event contains properties (timestamp, identification of the lead, information about their device / web browser, language, location etc). These events are meant to be stored by each tracking software so then it will be possible to get some monitoring.

Let's list a few tracking well-known tracking softwares :
* [Google Analytics]{:target="_blank"}{:rel="noopener noreferrer"}
* [Hotjar]
* [Mixpanel]
* [Amplitude]
* [Posthog]
* [Microsoft Clarity]
* [Segment]

We **do not recommend** to insert the tracking code of any of those softwares directly in your website / webapp. Instead, you should use [Google Tag Manager].

### Google Tag Manager

Why we recommend to use [Google Tag Manager] :
* Flexibility and speed : GTM offers a web console where you can dynamically add / remove tracking codes without touching the code ; the deployment takes 1s, and there is no impact on your code
* Consent mode : GTM offers a simple way to handle the consent mode for your visitors / users
* SEO : the pages load faster cause GTM injects the scripts asynchronously
* Maintenability : when a tracking software publishes a new version of their SDK, GTM notifies you, and you just need to update the template in the webconsole
* Historization : all changes made are logged in GTM, so you can see who changed what and when, and if necessary rollback the configuration
* No hassle : GTM is free, their SDK is extremely stable, and it doesn't retain data (no GDPR related issue)

## What to do with the data ?

The reason why you will probably need several softwares is because you don't have only 1 objective, right ?
Let's quickly review 3 main objectives :
* getting a broad understanding of **who** your leads are
* being able to very precisely check **what** they do
* getting to know **what you should do** to increase signups & conversions

### Who they are

Tracking softwares and analytics software can help on this.
[Google Analytics] is free, and will very quickly give you basic KPIs. You should probably plug it in GTM ([Google Tag Manager]).
[Mixpanel] and [Amplitude] are more flexible than [Google Analytics], as you can create your own charts. But they're also way more complex to setup, and require more of your time.

Anyways, those tools are limited to the information that is collected by the tracking code on the web browser (language, location, device...). Most of the time, it is not enough for you to assess whether or not a lead matches your ICP.
Hyperaktiv will solve this issue by enriching the data with information found on several online datasources (LinkedIn, YouTube, Twitch, OSINT..).

### What they do

To better understand what they do, the main feature you need to focus on are "session recording" and "heatmaps".
A few product analytics softwares provide these features : [Hotjar] is probably the most advanced, although [Amplitude], [Posthog] and [Microsoft Clarity] offer limited or paid options as well.
Based on our experience, these insights should be offered to the dev / product team ; but marketing / sales people might find the value provided by these tools very limited.

### What you should do

Here is the biggest weakness : it's "easy" to get the data to flow into analytics softwares, but it's really hard to know what to do in order to increase signups and conversions.
Hyperaktiv is 100% focused on giving you the right recommendations. Hyperaktiv collects the data gathered by the tracking infrastructure, enriches it with external datasources, and analyses the performance of your acquisition chanels, taking into account the engagement and ICP match of your leads.

How to setup requires only a few minutes ; let's start.

[Hotjar]: https://hotjar.com/{:target="_blank"}{:rel="noopener noreferrer"}
[Mixpanel]: https://mixpanel.com/
[Amplitude]: https://amplitude.com/
[Posthog]: https://posthog.com/
[Microsoft Clarity]: https://clarity.microsoft.com/
[Segment]: https://segment.com/
[Google Analytics]: https://analytics.google.com/
[Google Tag Manager]: https://tagmanager.google.com/
