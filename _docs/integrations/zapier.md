---
layout: docs
page: zapier
title: Zapier
description: Connect thousands of events to Engage through Zapier.
---

# Zapier

Engage's Zapier integration lets you send customer data and events from thousands of applications to Engage.

## How to connect

The Zapier integration is currently invite-only. You can request an invite by [clicking on the Zapier integration](https://zapier.com/developer/public-invite/126257/77e2d8fc01f13e16bc19b9ade8917470/) link in the integrations page on your Engage dashboard.

## Send customer data to Engage

To send customer attribute data from your choice application to Engage, follow the following steps:

- Create a new Zap.
- Search and Select the Trigger application.
- Select the event that contains the customer data you want to send to Engage.
- Search and select **Engage** as the Action application.
![Select Engage as Action application](/assets/images/docs/zapier-engage.png)
- Under **Action Event**, select **Update or Create a New Customer**.
![Update or Create a New Customer](/assets/images/docs/zapier-new-customer-2.png)
- Once you click **Continue**, you will be prompted to connect your Engage account (if not done already) by entering a username and password.
- Get your public and private API keys from your Engage dashboard (Settings -> Account -> Your API key).
- Enter your Public key as the username and the Private key as the password.
- Next, **Set up action**.
- Map the fields. Ensure that the **User ID** field is mapped to trigger application's user ID value. This ensures that subsequent events can be rightly mapped to the user.
![Map the fields](/assets/images/docs/zapier-customer-parameters.png)
- If there are extra customer attributes you want to track, you can use the **Extra attribute** fields. You can use this to add up to 5 additional customer attributes.
- To add an attribute, click on **Attribute name**. If you already have custom attributes sent to Engage, you can select them here. If not, click the **custom** tab and manually enter the attribute name, e.g., `customer_code`.
![Add extra attributes](/assets/images/docs/zappier-attrs.png)

## Send event data to Engage

To send customer events from your choice application to Engage, follow the following steps:

- Create a new Zap.
- Search and Select the Trigger application.
- Select the event that has the event data you want to send to Engage.
- Search and select **Engage** as the Action application.
- Under **Action Event**, select **Add Event**.
- Once you click **Continue**, you will be prompted to connect your Engage account (if not done already) by entering a username and password.
- Get your public and private API keys from your Engage dashboard (Settings -> Account -> Your API key).
- Enter your Public key as the username and the Private key as the password.
- Next, **Set up action**.
- Map the **User ID** field to the trigger application's user ID value. This is important as it helps Engage map the event to the right user. 
![Map User ID to the Paystack Customer ID](/assets/images/docs/zapier-setup-action.png)
- Next, click on the **Event** field. If you already have events in Engage, they will be listed here and you can select any of the listed events. If you have not sent any event to Engage, the list will be blank. Click on the **Custom** tab and you will be able to enter a custom event name.
![Add a custom event name](/assets/images/docs/zapier-custom.png)
- If the event has a single value or you are only interested in a single value, you can select the value in the **Event value** field.
- If however, you are interested in other properties of the events, you can use the **Property** fields for this. You can enter the name and value of up to 5 properties.
![Add additional properties](/assets/images/docs/zapier-ppties.png)