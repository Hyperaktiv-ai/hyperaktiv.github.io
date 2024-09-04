---
layout: default
title: Amplitude to Hyperaktiv 
parent: Tracking setup
nav_order: 4
description: "How to connect Hyperaktiv in Amplitude"
---
{% include variables.md %}
{% raw %}

# Integration with Hyperaktiv

1. Request an authentication key from us on [Slack community]
2. Create a project in [Amplitude] : 
   * [US based](https://app.amplitude.com/signup){:target="_blank"}{:rel="noopener noreferrer"}
   * [EU based](https://app.eu.amplitude.com/signup){:target="_blank"}{:rel="noopener noreferrer"}
3. Copy the API key, or leave the page open
4. Go to :
    1. "Data" in the top menu > "Destinations" > "Add destination"
    2. Search for "BigQuery"
    3. Check both checkboxes (it might be that the second one is not available yet, it's fine)
    4. Choose a frequency of 1h, then "Next"
    5. Dataset : put the name of your company
    6. Service Account key : upload the service account file we provided, then "Next"
    7. Data Destination Name : set "Hyperaktiv"

{% endraw %}

[Slack community]: https://join.slack.com/t/hyperaktivcommunity/shared_invite/zt-2gxxifo1f-N1lKn5~V32Hgvpx4~oi4IA
