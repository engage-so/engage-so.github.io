---
layout: docs
page: broadcasts
title: Sending broadcasts
description: Send targeted message campaigns to your customer groups through email, SMS, push notifications on mobile and web-in messaging on web.
---

# Sending broadcasts

Broadcasts are how you send manual messages to your customer [segments](/docs/guides/segments) and [lists](/docs/guides/lists). We currently supports the following channels for sending broadcasts:

1. Email
2. SMS
3. Push notifications (FCM)
3. Web in-app

More channels coming soon.

## Email

Sending an email broadcast requires configuring your domain or connecting an email service provider. If not yet done, you can do this from **Settings -> Integrations** on your account dashboard. If you choose to use Engage as your email service, we generate some DNS values to add to your domain's DNS. This is to allow you send emails using any email under the domain as sender.

The beauty of Engage is that we also let you bring your existing messaging infrastructure. If you already use any of the email service providers (ESP) we support, you can connect the service and use it for your email broadcasts (and [automations](/docs/guides/automations)). We currently support Amazon SES, Mailgun, Sparkpost and working on Postmark and Sendgrid. The other advantage of using your existing ESP is that we can provide you detailed analytics and reporting for your transactional emails and help you manage your [transactional email templates](/docs/guides/templates).

## SMS

You can send SMS broadcasts to your customer segments or lists. The broadcast will be sent to customers with phone numbers attached to their profile. At the moment, you will need to connect an SMS gateway to send SMS broadcasts. You can do this on the [Integrations page](https://app.engage.so/settings/integrations). We currently support Twilio, Termii , Africa's talking and Hollatags. More providers including Vonage and Infobip are coming shortly.

## Push notifications (FCM)

You can send push notifications to customer segments or lists by connecting your FCM account to Engage. This is availabile in **Settings -> Integrations** on your account dashboard. Before you can send push notification to a customer, remember that their device token needs to have been attached to their Engage profile. You can use the [user API](/docs/api/users) or any of the [available SDKs](https://engage.so/docs/sdks) to do this, i.e update the customer's `device_token` and `device_platform`. We currently store up to 5 device tokens per customer. When you send a broadcast, it is sent to all the device tokens connected to the customer's profile.

## Web in-app

You can send messages that display as a message popup at the bottom right of their customer's browser. You need to have installed the Engage JS SDK on web pages you want this to show up and identify/track the recipient on the page. If the recipient is online at the moment, the message immediately shows up. If they are not, it shows up when next they visit a page with the JS SDK. [Learn more](/docs/channels/web-inapp).
