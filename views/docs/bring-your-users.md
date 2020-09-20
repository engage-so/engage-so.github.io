---
layout: docs
---
# Bringing in your users

There are a couple of ways to bring your user data into Engage. 

## SDKs
An easy way to bring in user data is to use one of our [SDKs](/docs/sdks). The SDKs allows you add user data, update user attributes and track user events within your application. Even if you’ve added user data using other methods, the SDK is the best way to continually update user data from a one time integration.

## API
One of the biggest advantage of the API over the SDK is that you can use it to add user data and track past events for inactive users. If you are looking to send your user data to Engage without waiting for an active action from the user to trigger the SDK, the API is the way to go. Once you’ve used the API to import user data, you can then use the SDK to continually update the user data.

## Integrations
### Transactional email services
You can connect your Amazon SES or Mailgun to Engage. This will add all users you send transactional email to and mail attributes you can already segment them on. e.g number of opens, clicked links, bounces and mail subject. 
