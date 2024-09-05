---
layout: default
title: 3. Hyperaktiv with Amplitude
parent: Tracking setup
nav_order: 3
description: "How to connect Hyperaktiv in Amplitude"
---
{% include variables.md %}
{% raw %}

# Integrating Hyperaktiv and Amplitude

<iframe width="640" height="380" src="https://www.youtube.com/embed/moKX9NmFGw4?si=5Kvzvr7OEsosjHvn" title="How to connect Amplitude to Hyperaktiv" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen> </iframe>

1. Request an authentication key from us on [Slack community]
2. Create a project in [Amplitude] : 
   * [US based](https://app.amplitude.com/signup){:target="_blank"}{:rel="noopener noreferrer"}
   * [EU based](https://app.eu.amplitude.com/signup){:target="_blank"}{:rel="noopener noreferrer"}
3. Copy the API key, or leave the page open
4. In [Amplitude], go to :
    1. "Data" in the top menu > "Destinations" > "Add destination"
    2. Search for "BigQuery"
    3. Check both checkboxes (it might be that the second one is not available yet, it's fine)
    4. Choose a frequency of 1h, then "Next"
    5. Dataset : put the name of your company
    6. Service Account key : upload the service account file we provided, then "Next"
    7. Data Destination Name : set "Hyperaktiv"

# Next step >>

[4. Pushing events to GTM](/pages/GTM/Events)

{% endraw %}

