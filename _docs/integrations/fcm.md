---
layout: docs
page: fcm
title: FCM
description: Send your push notifications through Firebase Cloud Messaging (FCM)
---

# FCM

Engage lets you send push notifications using the [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) (FCM) Platform.

## How it Works

Engage connects to your Firebase account to send push notifications through broadcasts and automation to your customers. For this to work, the following requirements must be met.

1. You have a Firebase account. You can follow this [doc](https://firebase.google.com/docs/cloud-messaging) to create one.
2. You have integrated your Firebase account with Engage. You can do this via your Engage dashboard → Settings → Integrations → FCM.
3. You are tracking your users’ **device token** and **device platform**. The device token is how Engage and FCM is able to deliver the push notification to the targeted recipient. More on this later.

## Integration Steps

- Log in to your [Engage account](https://app.engage.so/settings) and visit the Settings page.
- Click on the **Integrations** tab.
- Click on the **Connect** button for Firebase. You will be directed to a page to enter upload your FCM key.
- Log in to Firebase and Generate a new private key by creating a new project - [Service Accounts](https://console.firebase.google.com/project/_/settings/serviceaccounts/adminsdk).
- Download the new key created.
- Upload the file on Engage.

## How to track device token and platform

As already mentioned, to be able to send push notifications, you need to track the user’s device token and platform. Engage allows you to track up to 5 tokens per user.

Before you can send the device token and platform to Engage, you need to get the token from the user’s device. The token is also generally referred to as **registration token**. FCM provides an easy way to get this within the mobile application. Here is how to across some development platforms:

- [Android](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register)
- [Flutter](https://firebase.google.com/docs/cloud-messaging/flutter/client#access_the_registration_token)
- [iOS](https://firebase.google.com/docs/cloud-messaging/ios/client#access_the_registration_token)

Once you get the device token, the next step is to send this to Engage. There are different ways to do this depending on how you integrate Engage with your mobile application or game.

- If you are using the Engage [User API](https://engage.so/docs/api/users), you can send the parameters `device_token` and `device_platform` when creating a user or updating the user’s attributes.
- If you are using the Flutter SDK, you can use the `setDeviceToken` method. More details in the [documentation](https://pub.dev/packages/engage/score).
- If you are using the Android SDK, you can use the `setDeviceToken` method. More details in the [documentation](https://github.com/engage-so/engage-android#set-device-token).
- If you are using [Segment](https://segment.com/docs/connections/destinations/catalog/engage-messaging/), ensure you are sending the device token to Segment. Using the Segment [Android library](https://segment.com/docs/connections/sources/catalog/libraries/mobile/android/android-faqs/#how-should-i-use-outbounds-push-notifications), you can do this via `putDeviceToken`. For [iOS](https://segment.com/docs/connections/sources/catalog/libraries/mobile/ios/ios-faqs/#how-do-i-use-push-notifications), you can do this with `registeredForRemoteNotifications`.

An example of tracked device token and platform can be seen below.

![Customer profile with device token](/assets/images/docs/device-token-example.png)