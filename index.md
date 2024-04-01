---
title: Home
layout: home
nav_order: 1
permalink: /
---

# Introduction

Hyperaktiv allows you to qualify your leads in real-time, and assign them a tailored customer onboarding journey.
Hyperaktiv offers a back-office where you can setup your workspace, an API given access to all your resources, and a front-office for your leads if you want them to be asked to complete activities.

# API

Base url for the API is ``https://app.hyperaktiv.ai/api/v1``.
You can find instructions on how to authenticate to our API [here](/pages/API%20authentication.html).
Our Postman collection can be used to facilitate tests on our API : [Hyperaktiv API on Postman](https://hyperaktiv.postman.co/workspace/Hyperaktiv~79462e29-fc9a-4b2c-8d41-bc662701b9da/collection/19855856-94cfa45e-58ff-4eeb-b1a3-7137759a6e4c?action=share&creator=19855856){:target="_blank"}{:rel="noopener noreferrer"}.
You can also browse and call our API with [SwaggerHub](https://app.swaggerhub.com/apis-docs/Hyperaktiv/api){:target="_blank"}{:rel="noopener noreferrer"}

# Terminology

## Roles

* Administrator : allows complete access to your workspace's back-office
* Manager : allows access to the whole back-office but workspace settings
* Lead : role assigned to new leads ; they have only access to the front-office, when activities are assigned to them
* Stakeholder : can be assigned to users who are not leads but who require and access to the front-office (they can even be external to your organization)

## Lead

A lead is a person who has been registered on Hyperaktiv ; the email of the lead is the key piece of information Hyperaktiv needs : depending on the information found online about the lead, the qualification algorithm implemented in Hyperaktiv will define the onboarding journey the lead will be assigned to, with tailored activities assigned.

## Funnel

A funnel is basically a workflow containing decision points, stages and activities. A stage is a group of Activities executed at the same time. Decisions allow you to define which stage should be triggered depending on specific conditions. Activities can be assigned to back-office users, leads, external stakeholders or automatically by Hyperaktiv. Here are a few examples of available activities : choosing a slot in Calendly, watching a video, verification of identity, signature of a document, etc.

## Journey

A journey is generated automatically by Hyperaktiv when a lead is assigned to a funnel. You can then track the progression of the customer onboarding journey through the back-office, and monitor which activities are blocked, completed or in progress. Once the journey is fully completed, the lead is considered "converted". Hyperaktiv offers analytics over completion and time spent of each activity.

## DataPoint

Journey-specific data is automatically made accessible by Hyperaktiv through data points. When the lead is registered, we automatically enrich data in the background based their email : revenue and size of their company, as well as the industry and sector, etc. You can also create your custom data points, and associate documents, text, amount, dates of any type of information to each journey. All data points associated to journey can be manipulated through the API, and be used in the lead qualification algorithm of the funnel aad fine-tune the customer onboarding journey.

## Session

You can create sessions through the API when you want to redirect your leads or external stakeholders to our front-office without asking them to use the login page. You can find more information about sessions [here](/Front-office%20session.html).
