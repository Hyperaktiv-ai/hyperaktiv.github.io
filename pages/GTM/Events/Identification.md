---
layout: default
title: User identification
parent: 4. Pushing events to GTM
grand_parent: Tracking setup
nav_order: 1
description: "How to track user identification"
---
{% include variables.md %}
{% raw %}

# User identification

<iframe width="640" height="380" src="https://www.youtube.com/embed/WLbw4u6O9t0?si=3F7-NIkiAjSM0rlS" title="How to identify your users with Google Tag Manager and Amplitude" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

As soon as your user is identified, their email should be pushed to Hyperaktiv and all tracking softwares.
This usually happens on signup and login.

# Push events to Google Tag Manager

## Signup
After a successful signup, add this piece of Javascript :
````
dataLayer.push({
  'event': 'signup',
  'provider': 'email',
  'user_email': 'johndoe@gmail.com',
  'user_id': '123456789'
});
````

(Replace "email" by "google" or any other SSO provider, "user_email" by the email of the user and "user_id" by the internal identifier of a user inside your product)

## Login
After a successful login, add this piece of Javascript :
````
dataLayer.push({
  'event': 'login',
  'provider': 'email',
  'user_email': 'johndoe@gmail.com',
  'user_id': '123456789'
});
````

# Send events from GTM to Amplitude

## Triggers
Create the following triggers with type ``Custom event`` :
- "Event - signup" :
	* Event name : ``signup``
- "Event - login" :
	* Event name : ``login``

## Variables
Create the following variables with type ``Data Layer Variable`` :
- "datalayer - provider"
	* Data Layer Variable Name : ``provider``
- "datalayer - user_email"
	* Data Layer Variable Name : ``user_email``
- "datalayer - user_id"
	* Data Layer Variable Name : ``user_id``

## Tags
Create the following tags with type ``Amplitude Analytics Browser SDK`` :
- "Amplitude - 'signup'" :
	* Tag type : ``Track Event (track)``
	* Event type : ``signup``
	* Individual Event Properties :
		* Property Name : ``provider``
		* Property Value : ``{{datalayer - provider}}``
	* Triggering : ``Event - signup``
- "Amplitude - 'login'" :
	* Tag type : ``Track Event (track)``
	* Event type : ``login``
	* Individual Event Properties :
		* Property Name : ``provider``
		* Property Value : ``{{datalayer - provider}}``
	* Triggering : ``Event - login``
- "Amplitude - setUserId" :
	* Tag type : ``Set User ID (setUserId)``
	* User ID : ``{{datalayer - user_id}}``
	* Triggering : ``Event - signup`` and ``Event - login``
- "Amplitude - identify" :
	* Tag type : ``Set User Properties (identify)``
	* Operation :
		* Method Call : ``Set``
		* User Property : ``user_email``
		* Value : ``{{datalayer - user_email}}``
	* Triggering : ``Event - signup`` and ``Event - login``

# Logout

It is recommended to also track your users logging out, so the session time can be computed with more accuracy.

## Push events to Google Tag Manager
When your user logs out, add this piece of Javascript :
````
dataLayer.push({
  'event': 'logout'
});
````

## Send events from GTM to Amplitude

## Triggers
Create the following triggers with type ``Custom event`` :
- "Event - logout" :
	* Event name : ``logout``

## Tags
Create the following tags with type ``Amplitude Analytics Browser SDK`` :
- "Amplitude - reset" :
	* Tag type : ``Reset User (reset)``
	* Triggering : ``Event - logout``

Everything is now ready.
Just use the "Preview" mode in GTM to check that all events are properly captured by GTM.

# Next step >>

[User activation](/pages/GTM/Events/Activation)

{% endraw %}
