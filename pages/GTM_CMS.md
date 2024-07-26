---
layout: default
title: GTM with a CMS
parent: Tracking setup
nav_order: 1
description: "How to use Google Tag Manager with a CMS"
---
{% include variables.md %}

# Introduction

If you're using a CMS (Content Management System), the installation of [Google Tag Manager] is specific.

## Bubble

Bubble offers the possibility to customize the ``header`` and the ``body`` only if you have a paid subscription. You can also use a (free) plugin

### In-house feature

1. Go to "Settings" > "SEO / metatags"
2. In section "SEO settings", you can customize the ``header`` and ``body``

### With a (free) plugin

1. Install [this plugin](https://bubble.io/plugin/google-tag-manager-1591196268063x958661259682644000) in your Bubble project
2. Go to "Plugins", and set your GTM container id (for example ``GTM-12345678``) in "GTM Container ID (headers)"

## Framer

1. In [Google Tag Manager], open the container you want to associate with your website (create one if none exists for this website), and click on ``Admin``, then ``Install Google Tag Manager`` ; keep this window open
2. In [Framer], go to ``Site Settings`` / ``General``, and scroll down to ``Custom Code``
3. Copy the script for the ``<head>`` section from [Google Tag Manager], and paste it in [Framer] configuration page
4. Copy the script for the ``<body>`` section from [Google Tag Manager], and paste it in [Framer] configuration page
5. Publish the [Framer] website
6. In [Google Tag Manager], test the installation.

## Webflow

Here is the [documentation](https://webflow.com/blog/integrating-google-tag-manager-with-google-analytics-in-webflow)

