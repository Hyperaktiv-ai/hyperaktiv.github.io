---
layout: default
title: GTM with a CMS
nav_order: 3
description: "How to use Google Tag Manager with a CMS"
---
{% include variables.md %}

# Introduction

If you're using a CMS (Content Management System), the installation of [Google Tag Manager] is specific.

## Framer

1. In [Google Tag Manager], open the container you want to associate with your website (create one if none exists for this website), and click on ``Admin``, then ``Install Google Tag Manager`` ; keep this window open
2. In [Framer], go to ``Site Settings`` / ``General``, and scroll down to ``Custom Code``
3. Copy the script for the ``<head>`` section from [Google Tag Manager], and paste it in [Framer] configuration page
4. Copy the script for the ``<body>`` section from [Google Tag Manager], and paste it in [Framer] configuration page
5. Publish the [Framer] website
6. In [Google Tag Manager], test the installation.

## Webflow

Here is the {documentation](https://webflow.com/blog/integrating-google-tag-manager-with-google-analytics-in-webflow)

