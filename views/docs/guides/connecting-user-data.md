---
layout: docs
page: bringing-users
title: Connecting user data
---
# Connecting user data

There are a couple of ways to connect your user data to Engage. 

## SDKs
An easy way to bring in user data is to use one of our [SDKs](/docs/sdks). The SDKs allow you add user data, update user attributes and track user events within your application. Even if you have added user data using other methods, the SDK is the best way to continually update user data from a one time integration.

## API
One of the biggest advantage of the [API](/docs/api) over the SDK is that you can use it to add user data and track past events for inactive users. If you are looking to send your user data to Engage without waiting for an active action from the user to trigger the SDK, the API is the way to go. Once you have used the API to import user data, you can then use the SDK to continually update the user data.

## Integrations
Integrations allow you connect services and tools you already use to Engage. This way, user data from the services can be automatically synced with Engage. We are working to allow connecting a lot of services and tools that you already use that are related to user events and attributes. Here are the currently supported ones:

### Transactional email services
You can connect your [Amazon SES](https://aws.amazon.com/ses) or [Mailgun](https://mailgun.com/) to Engage. This will add all users you send transactional email to and transactional email attributes you can already segment them on. e.g number of opens, clicked links, bounces and email subject. Engage also provides a transactional messaging module that allows you track deliveries, opens, clicks and failures of your transactional emails.

### Payment Gateways
If you use [Stripe](https://stripe.com/) for billing, you can connect your Stripe account to Engage. This will add automatically sync user payment events with Engage so that you can segment users on plans, amount spent, and related payment attributes. Support for other payment gateways coming soon.

### Notification services
You can connect services like [Slack](https://slack.com/) to get notified of failure deliveries and email complaints.
