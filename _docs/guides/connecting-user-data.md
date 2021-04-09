---
layout: docs
page: bringing-users
title: Connecting customer data
---

# Connecting customer data

Customer data forms the basis of everything you will be doing on Engage. Once you have connected your customer data to Engage, you can then

- [Segment customers](/docs/guides/segments) based on that data
- [Send manual broadcasts](/docs/guides/broadcasts) to customer segments
- [Send automated messages](/docs/guides/automations) based on different data driven triggers

This guide explains how this works and ways to connect your customer data.

## Types of customer data

With Engage, you can track two types of customer data—**attributes** and **events**. Attributes are generally distinctive user properties like gender, location or even plan name. Events are actions users perform within your application like clicking a button, visiting a page or placing an order. This seems quite straightforward but because Engage allows you track anything as an attribute and anything as an event, the difference can quickly get blurry. 

As an example, when a user upgrades their plan, you can either track the new plan's name as an attribute or the upgrade action with plan details as an event. Either works depending on how you want to later use that information. If you need to later segment your customers by when they upgrade or how many upgrades they have done, then tracking as an event is the better option. If you only need to know the customer's current plan at any time, then tracking as an attribute it is.

Generally, if you do not need to track changes to the data and you want the data visible in the customer's page on your Engage dashboard, then track as an attribute. When you track an attribute, the value overwrites the previous value if one exists. In order words, only the latest value is stored. If you want to track changes to the data over time, then track as an event. Engage stores each event data with date so you can do things like segment user data by that event and date or number of occurrence.

For communication and identification, we use some attributes as provided by you. Internally, we call these **standard attributes**. They are:

- `first_name` - The user's first name. We use this primarily for identification
- `last_name` - The user's last name. We use this primarily for identification
- `number` - The user's phone number in international format (numbers only). When you initiate a send-sms event through broadcast or automation, this is the property we send it to.
- `email` - The user's email. When you initiate a send-email event either through broadcast or automation, this is the property we send it to.
- `device_token` - A unique identification number linked to the user's device. When you initiate a send-push notification event either through broadcast or automation, this is the property we send it to. Engage tracks up to 5 device tokens and platform for each customer.
- `device_platform` - The mobile device platform the device token is gotten from. Value is either `ios` or `android`

## Knowing what data to bring in

You only need to connect important data needed for communication or data analysis to Engage. Let's take an hypothetical internet service provider (let's call it MInt) and look at how this will be done, starting with attributes.

The first step is to start by creating a list of user attributes you collect for your customers. It might also help to also note where the attribute is collected. For MInt, this will be:

- Name - onboarding
- Email - onboarding
- Address - onboarding
- Plan - on upgrade or change of plan
- Current usage for the month - at regular intervals, hourly maybe
- Signup date - onboarding

Next, review your list and strike out attributes that you will not need for customer messaging. The attributes list for MInt looks good so far, so no need to strike anything out. The name will be useful for identifying the customer. Email is where messages will be sent. The plan name is good for targeting customers in particular plans–we may need to give them additional features and tell them about it. Same for address. If there is a downtime in an area, we can send a broadcast to notify people in that location. We may not need usage for communication but we can create a segment for users above a particular threshold for data analysis. We can even use create an automation to automatically send a notification of high usage when they enter the segment. We can also create an automation to automatically check in and ask if everything is good if after a week, usage is below a threshold.

For event tracking, we will follow the same steps. Once we have our event list, we can narrow down to the important customer actions/events:

- Added a family member to plan
- Purchased additional bandwidth

## How to bring the data in

Now that we know what data to bring in, how do we do it? 

Engage provides a couple of ways to easily connect your user data. 

### Direct import

You can directly import your customer data from the user page of the Engage dashboard by uploading a CSV file. Download your users data as a CSV file from your datastore, including all necessary attributes that will be useful for segmentation. These could be gender, date of birth, location, product plan, etc. Upload the file and you can immediately start segmenting your users based on the uploaded attributes.

The direct import is a quick way to get started but there are two drawbacks. 

1. You can only import attributes with this method. You cannot use the method to bring in customer event data.
2. The data is not live. Because it is not connected to a source, if there are changes to the data at the source, there is no way to automatically update in Engage. It has to be manually done.

### Integrations

Integrations are the easiest way to get your customer data into Engage. Integrations allow you connect services and tools you already use to Engage. These tools are then used to sync and enrich your customer data, power your messaging through Engage or notify you of delivery events. At the moment, Engage has two major types of integrations that sync customer in–**transactional email services** and **payments gateways**. We are working to allow connecting a lot of services and tools that you already use that are related to user events and attributes. A list of supported services is available on the [Integrations page](https://app.engage.so/settings/integrations) of the Engage dashboard.

### SDKs

Another easy way to bring in user data is to use [one of the SDKs](/docs/sdks). The SDKs allow you add user data, update user attributes and track user events within your application. Even if you have added user data using other methods, the SDK is an easy way to continually update user data from a one time integration.

### API

Using the [API](/docs/api) gives you the best flexibility. One of the biggest advantage of the API over the SDKs is that you can use it to add user data for inactive users and track past events. If you are looking to send your user data to Engage without waiting for an active action from the user to trigger the SDK, the API is the way to go. Once you have used the API to import user data, you can then use the SDK to continually update the user data.
