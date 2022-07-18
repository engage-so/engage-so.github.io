---
layout: docs
page: onesignal
title: OneSignal
description: Send your push notifications through OneSignal
---

# OneSignal

Engage's OneSignal integration lets you send your mobile push notifications through [OneSignal](https://onesignal.com/). 

## How it works

We connect to your OneSignal account to send your push notifications for Broadcasts or Automations. For this to work, there are some expectations:
1. You have already [integrated OneSignal with your application](https://documentation.onesignal.com/docs/integrations) and sending your customer data to OneSignal.
2. You have already integrated Engage and already sending your customer data to Engage
3. You [set an external user Id](https://documentation.onesignal.com/docs/external-user-ids) for customer data added to OneSignal. If you are already setting other custom user properties, adding the external user Id property doesn't affect anything. Infact, OneSignal highly recommends this.
4. You are using the same user Id to identify customers on Engage. (See the [User API](/docs/api/users) or [SDKs](/docs/sdks) on identifying or tracking events with the user Id).

## How to integrate OneSignal

![Connect OneSignal to Engage](/assets/images/docs/onesignal-2.png)

- Log in to your [Engage account](https://app.engage.so/settings) and visit the Settings page.
- Click on the **Connect** button for OneSignal. You will be directed to a page to enter your App ID and Rest API Key.
- Log in to your OneSignal account and visit the Settings page.
- Copy your APP ID and Rest API Key and paste in the Engage's OneSignal integration page.
- Click the **Continue** button to complete the integration. You should get a successful notification.


## Sending a push notification on Engage with OneSignal

![Select OneSignal as the send service](/assets/images/docs/onesignal.png)

- Select Push Notification when you want to create a new Broadcast or Automation action
- Under **Service** or **Send using**, select **OneSignal**
- Compose your message
- Send, Save or Schedule

