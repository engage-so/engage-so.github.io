---
layout: docs
page: ps
title: Paystack Integration
description: Connect your Paystack account to Engage for your messaging campaigns and automation based on your customers' billing events.
---

# Paystack

Engage connects to your [Paystack account](https://paystack.com) to let you create customer segments based on your customer’s billing events and automate messaging using these events.

## How to connect

- Visit the [Integrations page](https://app.engage.so/settings/integrations) of your Engage dashboard and click on Paystack
- Enter your Paystack live secret keys. We use this to sync your existing Paystack customers to Engage.
- Click **Complete Setup**. A unique URL will be generated for you. You will need to update your Paystack **Live Webhook URL** with this.
- Login to your [Paystack dashboard](https://dashboard.paystack.com/#/login)
- Navigate to the **Settings** page on your dashboard
![Paystack Settings](/assets/images/docs/ps-settings.png)
- Update your Paystack **Live Webhook URL** with the unique URL generated for you.
![Settings](/assets/images/docs/ps-save.png)
- If you already have another URL in the **Live Webhook URL** field, you can use our [Zapier integration](#connecting-through-zapier) instead. Details below.
- Once done, click the **Save Changes** button

## Events we support
We currently support 7 [Paystack events](https://paystack.com/docs/payments/webhooks/#types-of-events) directly. They are:
- **Charge successful** (`charge.success`)   
Triggered when there is a successful one time charge.
- **Subscription renewal successful**   
Triggered when there is a successful subscription renewal.
- **Storefront charge successful**   
Triggered when there is a successful storefront purchase/order.
- **New customer subscription** (`subscription.create`)   
Triggered when there is a new customer subscription.
- **Customer subscription deleted** (`subscription.disable`)   
Triggered when a subscription is disabled.
- **Customer identification successful** (`customeridentification.success`)   
Triggered when a customer identification is successful.
- **Customer identification failed** (`customeridentification.failed`)   
Triggered when a customer identification fails.

More events are available through the Zapier integration.

## Data we collect
We collect the standard attributes `first_name`, `last_name`, `email` and `number` for every customer. For the supported Paystack events, we collect event-specific data you can use for filters when creating customer segments and as [personalization tags](/docs/guides/tags) within your automation messages. 

### Event data

- `amount` - Transaction amount. Available in all payment related events. 
- `status` - Transaction status. Available in all payment related events. 
- `ip_address` - The IP address of the request.
- `currency` - Currency ISO (all caps). Available in all payment related events. 
- `referrer` - The referrer page for the transaction.
- `fees` - Transaction fees. Available in all payment related events. 
- `plan_id` - The ID of the plan. Available in all subscription events.
- `plan_name` - The plan name. Available in all subscription events.
- `plan_amount` - The plan amount. Available in all subscription events.
- `plan_currency` - Currency ISO (all caps). Available in all subscription events.
- `renewal_date` - Subscription renewal date. Available in new subscription event.
- `order` - An array containing details of order items. Each array will include an object of the keys:
  - `id` - The product ID
  - `name` - The product name
  - `quantity` - The quantity of product
  - `amount` - The unit amount of the product


> Important note: For easier use, `amount` and `fees` are converted from the smallest unit sent by Paystack to a hundredth. For example, if Paystack sends 10000 (kobo) for a Naira payment, we convert it to 100. Engage’s personalization tag engine is built on [Liquid template language](https://shopify.github.io/liquid/), so you can multiply by 100 to convert back, e.g {%raw%}`{{ event.amount | times: 100 }}`{%endraw%}

## Using event data for personalization tags
If an automation trigger is **Event is triggered** and the event type is a **Paystack event**, you can use any of the Paystack event data above as a personalization tag within messages in the automation. To do this, prefix with `event.`.

Remember, Engage’s personalization tag engine is built on [Liquid template language](https://shopify.github.io/liquid/), so you can use this to format your tags. 

Here is an example:

{% raw %}
```
Here is a summary of your storefront order:
{% for item in event.order %}
{{item.name}} - {{item.quantity}} x {{item.amount}}
{% endfor %}
Total: ${{event.amount}}
Have questions? Reply this email.
```
{% endraw %}

## Connecting through Zapier

Besides using the Live webhook URL, you can also connect your Paystack to Engage through Zapier. Our Zapier integration is currently invite-only. You can request an invite by [clicking on the Zapier integration](https://zapier.com/developer/public-invite/126257/77e2d8fc01f13e16bc19b9ade8917470/) link in the integrations page on your Engage dashboard.

To help Engage identify new customers in your Paystack account, we recommend you start by connecting the **New Customer** Paystack event on Zapier to Engage. Here is how:

- Create a new Zap.
- Search and Select **Paystack** as the Trigger application.
- Select the event: **New Customer**.
![Select the event: New Customer](/assets/images/docs/zapier-new-customer.png)
- Search and select **Engage** as the Action application.
![Select Engage as Action application](/assets/images/docs/zapier-engage.png)
- Under **Action Event**, select **Update or Create a New Customer**.
![Update or Create a New Customer](/assets/images/docs/zapier-new-customer-2.png)
- Once you click **Continue**, you will be prompted to connect your Engage account (if not done already) by entering a username and password.
- Get your public and private API keys from your Engage dashboard (Settings -> Account -> Your API key).
- Enter your Public key as the username and the Private key as the password.
- Next, **Set up action**.
- Map the fields to the right Paystack value. Ensure that the **User ID** is mapped to the Paystack customer's ID.
![Map the fields](/assets/images/docs/zapier-customer-parameters.png)
- If there are extra customer attributes you want to track, you can use the **Extra attribute** fields. You can use this to add up to 5 additional customer attributes.
- To add an attribute, click on **Attribute name**. If you already have custom attributes sent to Engage, you can select them here. If not, click the **custom** tab and manually enter the attribute name, e.g., `customer_code`.
![Add extra attributes](/assets/images/docs/zappier-attrs.png)

To send a Paystack event to Engage through Zapier:

- Create a new Zap.
- Select **Paystack** as the Trigger application.
- Select the event.
- Search and select **Engage** as the Action application.
- Under **Action Event**, select **Add Event**.
- In the **Set up action** section, click the **User ID** field and select **Customer ID** from the list of Paystack data.
![Map User ID to the Paystack Customer ID](/assets/images/docs/zapier-setup-action.png)
- Next, click on the **Event** field. If you already have events in Engage, they will be listed here and you can select any of the listed events. If you have not sent any event to Engage, the list will be blank. Click on the **Custom** tab and you will be able to enter a custom name for the Paystack event.
![Add a custom event name](/assets/images/docs/zapier-custom.png)
- If the event has a single value or you are only interested in a single value, you can select the value in the **Event value** field. If for example the Paystack event is **Abandoned Cart** and you are only interested in the amount, you can set this as the event value.
![Select event and event value](/assets/images/docs/zapier-ps-event-value.png)
- If however, you are interested in other properties of the events, you can use the **Property** fields for this. You can enter the name and value of up to 5 properties.
![Add additional properties](/assets/images/docs/zapier-ppties.png)

Important note: The events you send through Zapier will not be available in **Paystack events** when selecting condition filter category in Segments or Automations. They will be available under **Events**. Only events tracked using the **Live Webhook URL** option will be available in **Paystack events**.

![Zapier events will be available through "Events" and not "Paystack Events"](/assets/images/docs/zapier-condition-filters.png)