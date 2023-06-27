---
title: Home
layout: home
nav_order: 1
permalink: /
---

# Introduction

Kohomai allows you to qualify your leads in real-time, and assign them a tailored customer onboarding journey.
Kohomai offers a back-office where you can setup your workspace, an API given access to all your resources, and a front-office for your leads if you want them to be asked to complete activities.

# API

Base url for the API is ``https://app.kohomai.com/api/v1``.
You can find instructions on how to authenticate to our API [here](/pages/API%20authentication.html).
Our Postman collection can be used to facilitate tests on our API : [Kohomai API on Postman](https://kohomai.postman.co/workspace/Kohomai~79462e29-fc9a-4b2c-8d41-bc662701b9da/collection/19855856-94cfa45e-58ff-4eeb-b1a3-7137759a6e4c?action=share&creator=19855856).
You can also browse and call our API with [SwaggerHub](https://app.swaggerhub.com/apis-docs/Kohomai/api/1.0.0){:target="_blank"}{:rel="noopener noreferrer"}

# Terminology

## Roles

## Lead

A lead is a person who has been registered on Kohomai ; the email of the lead is the key piece of information Kohomai needs : depending on the information found online about the lead, the qualification algorithm implemented in Kohomai will define the onboarding journey the lead will be assigned to, with tailored activities assigned.

## Funnel

A funnel is basically a workflow containing decision points, stages and activities. A stage is a group of Activities executed at the same time. Decisions allow you to define which stage should be triggered depending on specific conditions. Activities can be assigned to back-office users, leads, external stakeholders or automatically by Kohomai. Here are a few examples of available activities : choosing a slot in Calendly, watching a video, verification of identity, signature of a document, etc.

## Journey

A journey is generated automatically by Kohomai when a lead is assigned to a funnel. You can then track the progression of the customer onboarding journey through the back-office, and monitor which activities are blocked, completed or in progress. Once the journey is fully completed, the lead is considered "converted". Kohomai offers analytics over completion and time spent of each activity.

## DataPoint

Journey-specific data is automatically made accessible by Kohomai through data points. When the lead is registered, we automatically enrich data in the background based their email : revenue and size of their company, as well as the industry and sector, etc. You can also create your custom data points, and associate documents, text, amount, dates of any type of information to each journey. All data points associated to journey can be manipulated through the API, and be used in the lead qualification algorithm of the funnel aad fine-tune the customer onboarding journey.

## Session

You can create sessions through the API when you want to redirect your leads or external stakeholders to our front-office without asking them to use the login page. You can find more information about sessions [here](/front-office%20session.html).
