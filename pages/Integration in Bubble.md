---
layout: default
title: Integration in Bubble
nav_order: 4
description: "How to integrate Hyperaktiv in Bubble"
---
{% include variables.md %}

# How to integrate Hyperaktiv in Bubble

You have 2 options to register leads in Hyperaktiv using your [Bubble]{:target="_blank"}{:rel="noopener noreferrer"} website :
* Simplified version : you can install our plugin (limited features : it's not possible to send custom data points)
* Advanced version : you have to install the API connector plugin, and have access to all capabilities of Hyperaktiv API.

## Simplified : Hyperaktiv plugin
In your [Bubble]{:target="_blank"}{:rel="noopener noreferrer"} app, go to "Plugins" on the left navigation panel, then click on "Add plugins" on the top right of the screen. Search "Hyperaktiv" plugin, and click "Install".

In the plugin page, set the following values :
* API key : ``Bearer [YOUR_API_KEY]`` _(replace [YOUR_API_KEY] by the API key which is displayed in Hyperaktiv/Settings/API, or in the "API origin" page)_

## Advanced : API Connector plugin
In your [Bubble]{:target="_blank"}{:rel="noopener noreferrer"} app, go to "Plugins" on the left navigation panel, then click on "Add plugins" on the top right of the screen. Search "API Connector" plugin, and click "Install".

In the plugin page, click on "Add another API", and set the following values :
* API Name : ``Hyperaktiv`` _(you can use another name)_
* Authentication : ``Private key in header``
* Key name : ``Authorization``
* Key value : ``Bearer [YOUR_API_KEY]`` _(replace [YOUR_API_KEY] by the API key which is displayed in Hyperaktiv/Settings/API, or in the "API origin" page)_

Click on "Add a shared header", and set :
* Key : ``Content-Type``
* Value : ``application/json``

Click on "expand" next to the "API call" which was automatically created, and set :
* Name : ``Register a lead`` _(you can use another name)_
* Use as : ``Action``
* Data type : ``JSON``
* Method : ``POST``
* URL : ``https://app.hyperaktiv.ai/api/v1/leads?ref=XXX`` _(where XXX is the reference of the "API origin" in your funnel)_
* Body type : ``JSON``
* Body : ``{"Email": "<email>", "Firstname": "<firstname>", "Lastname": "<lastname>", "PhoneNumber": "<phoneNumber>"}``
* Body parameters : 4 keys should have been created : ``email``, ``firstname``, ``lastname``, ``phoneNumber`` ; leave the values empty, but uncheck "private" for all parameters.
* Include errors in response and allow workflow actions to continue : ``yes``
* Capture response headers : ``yes``

## Use the plugin in your [Bubble]{:target="_blank"}{:rel="noopener noreferrer"} workflow

Go to the workflow you want to use to call Hyperaktiv, and click on "Click here to add an action...". In the drop down menu, go to "Plugins", and select "Hyperaktiv - Register a lead" (or whatever you previously set as a name).

Set the parameters values for the API call in the contextual popup of this step.
* The ``email`` parameter is mandatory, so you will have to map this parameter with a textfield in your webpage ; for example, if your textfield is called "emailTextfield", you have to set the parameter value "Input emailTextfield's value".
* The ``ref`` parameter is mandatory, you should set a static value here (it's the id of the "API origin")
* You can leave other parameters blank, or you can also map them to textfields value if they exist in your form.

[Bubble]: https://bubble.io
