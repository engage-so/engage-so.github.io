---
layout: docs
page: ps
title: Paystack Integration
---

# Paystack

Engage integrates with [Paystack](https://paystack.com/) to sync your customer data and track customer payment events.

To connect your Paystack account,

- Visit the [Integrations page](https://app.engage.so/settings/integrations) of your Engage dashboard and click on Paystack
- Enter your Paystack live secret keys.
- Login to your [Paystack dashboard](https://dashboard.paystack.com/#/login)
- Navigate to the **Settings** page on your dashboard
![Paystack Settings](/assets/images/docs/ps-settings.png)
- Confirm the **Live Webhook URL** field is empty. If it is, set the value to
- If the field is not empty, your developer will need to update the existing webhook script to use the necessary events but also directly send the events from Paystack to https://api.engage.so/webhooks/paystack/{{acc_active_domain._id}}
- If you need more help, we will be glad to help with concierge integration. Please send a mail to [hello@engage.so](mailto:hello@engage.so)
![Settings](/assets/images/docs/ps-live.png)
- Once done, click the **Save Changes** button
![Settings](/assets/images/docs/ps-save.png)
