---
title: Home
layout: home
nav_order: 1
permalink: /
---

# Introduction

Hyperaktiv helps you increase conversion by segmenting your leads based on :
* their engagement on your website / app
* how much they match your ICP (Ideal Customer Profile)

Hyperaktiv offers a back-office where you can automate actions, but also monitor your funnel, and get a better understanding of who are your leads.
In order to analyse the performance of your funnel, we'll capture everything your website's visitors and app users do, thanks to a simple tracking infrastructure.

# Tracking infrastructure

We can implement the tracking infrastructure for you (just ping us on [Slack]), or you can implement it by yourself using this [documentation](/pages/Tracking_principles)

# API

Base url for the API is ``https://app.swaggerhub.com/apis-docs/Hyperaktiv/api``.
You can find instructions on how to authenticate to our API [here](/pages/API).
Our Postman collection can be used to facilitate tests on our API : [Hyperaktiv API on Postman](https://hyperaktiv.postman.co/workspace/Hyperaktiv~79462e29-fc9a-4b2c-8d41-bc662701b9da/collection/19855856-94cfa45e-58ff-4eeb-b1a3-7137759a6e4c?action=share&creator=19855856){:target="_blank"}{:rel="noopener noreferrer"}.
You can also browse and call our API with [SwaggerHub](https://app.swaggerhub.com/apis-docs/Hyperaktiv/api){:target="_blank"}{:rel="noopener noreferrer"}

# Terminology

## Goals

Hyperaktiv lets you choose what is the current focus of your business strategy :
* Acquisition : increasing the amount of (good quality) leads in your funnel
* Retention : increasing the engagement of signups
* Conversion : increasing the amount of paying customers

## Lead

A lead is a person who has been visiting your website

## User

A lead who created an account on your product

## Stage

Defines the life cycle of a Lead :
* Visitor : when they have anonymously visited the website
* Signup : when they created an account
* Trial : when they started a trial
* Converted : when they made a purchase

## Segment

We classify leads in 4 different segments, depending on their :
* engagement score : how much a lead is interested / invested in your website / app (relatively amongst the leads of the same stage)
* ICP match : how much they match your Ideal Customer Profile

There are 4 segments :
* Champions : high engagement score, high ICP match
* Regulars : high engagement score, low ICP match
* Explorers : low engagement score, high ICP match
* Strangers : low engagement score, low ICP match

Hyperaktiv gives you recommendations to increase engagement of current leads, and increase the acquisition of Champions

## Workflow

A workflow is a set of automated actions which are executed automatically when a Lead reaches a new stage.

## DataPoint

Any piece of information related to a lead.

## Enrichment

Hyperaktiv can fetch information about your Leads (based on their email), in order to compute their ICP match, and give you better insights

[Slack community]: https://join.slack.com/t/hyperaktivcommunity/shared_invite/zt-2gxxifo1f-N1lKn5~V32Hgvpx4~oi4IA
