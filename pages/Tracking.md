---
layout: default
title: Tracking infrastructure
nav_order: 4
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
If you want to directly jump to the step-by-step installation, it's [here]()

# Which tools ?

There are a few great tools on the market today. But unfortunately, not one of them can cover all your needs.
Let's start here : let's dissociate "how/what to track" from "what to do with the data"

## How/what to track
On your website / webapp / mobile app, every time a lead is performing an action (opening a page, clicking on a button ...), an event will be recorded. This event will contain properties (timestamp, identification of the lead, information about their device / web browser, language, location etc). These events are meant to be stored by each tracking software so then it will be possible to get some monitoring.

Let's list a few tracking well-known tracking softwares :
* [Google Analytics]
* [Hotjar]
* [Mixpanel]
* [Amplitude]
* [Posthog]
* [Microsoft Clarity]
* [Segment]

But before diving into each of them, let's set a first principle :
As you will probably need (right away, or later) several, **you don't want to hard-code each of their specific SDK in your website / app**.
This would lead to frequent updates, bug fixes -> higher maintenance cost and technical complexity.
Instead, we strongly recommend to use [Google Tag Manager] on your website and app to manage all your tracking snippets dynamically.
[Google Tag Manager] is free, lightweight, and very stable (no code changes). Your dev team will be happy with it.
Plus you will be able to activate / deactivate / add / configure tracking softwares dynamically with a web-based console, **without any code change**.

## What to do with the data ?

The reason why you will probably need several softwares is because you don't have only 1 objective, right ?
Let's quickly review 3 main objectives :
* getting a broad understanding of **who** your leads are
* being able to very precisely check **what** they do
* getting to know **what you should do** to increase signups & conversions

### Who they are

Tracking softwares and analytics software can help on this, for sure.
[Google Analytics] is free, and will very quickly give you basic KPIs. You should probably plug it in GTM ([Google Tag Manager]).
[Mixpanel] and [Amplitude] are more flexible than [Google Analytics]

### What they do

### What you should do


[Hotjar]: https://hotjar.com/
[Mixpanel]: https://mixpanel.com/
[Amplitude]: https://amplitude.com/
[Posthog]: https://posthog.com/
[Microsoft Clarity]: https://clarity.microsoft.com/
[Segment]: https://segment.com/
[Google Analytics]: https://analytics.google.com/
[Google Tag Manager]: https://tagmanager.google.com/
