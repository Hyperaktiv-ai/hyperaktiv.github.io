---
layout: default
title: UTM
nav_order: 5
description: "UTM Parameters in action"
---
{% include variables.md %}

# Introduction to UTM Parameters
* **Definition**: UTM parameters are short text codes added to URLs to track the performance of marketing campaigns, and keep track of the source of the traffic in general.
* **Origin**: UTM stands for "Urchin Tracking Module", originating from Urchin, a predecessor to Google Analytics. It is not an officail WEB standard, but it became some sort of standard de facto.

# Why UTM Parameters matter
* **Accurate Attribution**: Assign precise credit to traffic sources, understanding which platforms drive the most traffic.
* **Measuring Campaign Performance**: Analyze metrics like conversions, bounce rates, and time on-site for various campaigns.
* **Calculating ROI**: Determine the return on investment by tracking traffic and conversions from each channel.
* **Audience Segmentation**: Segment visitors based on traffic sources to tailor content more effectively.
* **Data-Driven Decisions**: Use insights to refine social media strategies and allocate budgets more efficiently.

# How to Create UTM Parameters
Parameters are simply appended in a URL after a ``?``, separated by ``&`` (e.g., ``http://www.example.com/?utm_source=facebook&utm_medium=paid_social&utm_campaign=summer_sale``).
## UTM Parameters Overview:
### Mandatory parameters:
* **Campaign Source (``utm_source``)**: Identifies the traffic source (e.g., facebook, twitter, google).
* **Campaign Medium (``utm_medium``)**: Specifies the channel (e.g., social, cpc, email).
* **Campaign Name (``utm_campaign``)**: Name the campaign (e.g., summer_sale, product_launch).
### Optional parameters:
* **Campaign Identifier (``utm_id``)**: It is a good practice to use this field to identify campaigns in Google Ads / Google Analytics or other softwares.
* **Campaign Term (``utm_term``)**: Tracks keywords (often used in paid search ads).
* **Campaign Content (``utm_content``)**: Differentiates between multiple links or creatives (e.g., ad1, ad2).

# Advices for using UTM Parameters
* **Apply the standards**: Use tools like [UTM builder](https://utmbuilder.net/){:target="_blank"} to create URL with UTM parameters quickly.
* **Commitment**: Use UTM parameters everywhere there is a link to your website: blogs, social medias, emails, ads...
* **Avoid Internal Links**: Do not use UTM parameters for internal links to prevent tracking errors.
* **Document Naming Conventions**: Create a consistent system for naming UTM parameters to avoid discrepancies.
* **Maintain Consistency**: Use lowercase, avoid spaces, and choose consistent separators in UTM parameters.
* **Check for Errors**: Regularly review UTM codes for mistakes or typos.
* **Track Links in a Spreadsheet**: Manage and document UTM links to avoid duplication and ensure easy reference.
* **Track ROI**: Use unique UTM parameters to measure performance and ROI.
* **Experiment with A/B Testing**: Test different content or strategies using UTM parameters to find what works best.
* **Create Campaign Presets**: Use tools like [Hootsuite](https://www.hootsuite.com/){:target="_blank"} to save and apply UTM parameters quickly and consistently.

# How to automatically add UTM parameters to my Google Ads campaigns / ads ?
* ``Admin`` > ``Account Settings`` > ``Tracking``
* set this in "Final URL suffix" : ``utm_source=google&utm_medium=cpc&utm_campaign={campaignid}&utm_content={adgroupid}&utm_term={keyword}``
All ads will now have UTM parameters
