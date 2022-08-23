---
layout: docs
page: stripe
title: Stripe Integration
description: Connect your Stripe.com account to Engage for your messaging campaigns and automation based on your customers' billing events.
---

# Stripe
Engage connects to your [Stripe account](https://stripe.com) to let you create customer segments based on your customer’s billing events and automate billing messages using these events. For example, you can use Engage to automatically send customers email when they have an upcoming invoice or remind them their trial will expire soon. 

## How to connect
Visit the **Settings** page of your Engage dashboard and click on the **Integrations** tab. Scroll down to the **Payment** category and click the **Stripe** connect button. You will be redirected to Stripe to authorise your preferred account with Engage. Engage only gets read permission to receive the supported event and nothing more.

## Events we support
We currently support 16 [Stripe events](https://stripe.com/docs/api/events/types). They are:
- **Customer created** (`customer.created`)   
This is triggered when a new customer is created on Stripe. This mostly happens when a customer attempts payment by adding a payment source like a card.
- **Invoice created** (`invoice.created`)   
Stripe triggers invoice created when a new invoice is created. You can use this to trigger an automation that sends invoice payment reminders over a period of weeks.
- **Invoice upcoming** (`invoice.upcoming`)   
Stripe triggers invoice upcoming events before a subscription is charged and renewed. (You can customise when on your Stripe dashboard). You can use this to automate reminders of an upcoming invoice charge for example.
- **Invoice payment successful** (`invoice.payment_succeeded`)   
This is triggered when an invoice is paid.
- **Invoice paid** (`invoice.paid`)   
This is triggered when an invoice is paid. The difference between this event and **Invoice payment successful** is that this is additionally triggered when the invoice is marked as paid on the Stripe dashboard. Both events are therefore sometimes triggered for the same invoice.
- **Invoice payment failed** (`invoice.payment_failed`)   
This is trigged when an invoice payment fails.
- **Invoice deleted** (`invoice.deleted`)   
This is trigged when an invoice is deleted.
- **Invoice voided** (`invoice.voided`)   
This is trigged when an invoice is marked as void on the Stripe dashboard.
- **Invoice marked uncollectible** (`invoice.marked_uncollectible`)   
This is trigged when an invoice is marked as uncollectible on the Stripe dashboard.
- **Charge failed** (`charge.failed`)   
This is triggered when a charge fails.
- **Charge successful** (`charge.succeeded`)   
This is triggered when a charge is successful.
- **New customer subscription** (`customer.subscription.created`)   
This is triggered when a customer subscribes to a new subscription. You can use this to automate "Thank you" notifications for example.
- **Subscription deleted** (`customer.subscription.deleted`)   
This is triggered when a customer’s subscription is canceled. 
- **Trial will end** (`customer.subscription.trial_will_end`)   
This is triggered when a customer’s trial period for a subscription will end. You can use this to send reminders for cancelation. It is a good practice to remind customers that their trial will expire and they will be billed.
- **Card will expire** (`customer.source.expiring`)   
This is triggered when a customer card will expire at the end of month. We only support this for card expiry and not other customer payment methods. Use this to send reminders to customers to update their billing details.
- **Checkout session expired** (`checkout.session.expired`)   
This is triggered when a customer leaves a checkout page and the session expires. This is popularly called **Abandoned Cart** in e-commerce. Use this to send reminders to customers about their pending order. [Learn more](https://stripe.com/docs/payments/checkout/abandoned-carts).

## Data we collect
We collect different data for the supported events so you can use them to create customer segments and use them as [personalization tags](/docs/guides/tags) within your automation messages. 

Important note: For easier use, the amount data is converted from the minor unit sent by Stripe to the monetary unit. For example, Stripe sends 100 (Cent) for a dollar payment but we convert it to 1 (Dollar). Engage’s personalization tag engine is built on [Liquid template language](https://shopify.github.io/liquid/), so you can multiply by 100 to convert back, e.g {%raw%}`{{ event.amount | times: 100 }}`{%endraw%}

### Event data

> Note: To use as personalization tags, prefix with `event.` e.g `event.amount`.

- `invoice_url` - A URL to view (and pay) for invoice if finalised. Available in the invoice events: Invoice created, Invoice upcoming, Invoice paid, Invoice payment successful, Invoice payment failed, Invoice voided, Invoice marked uncollectible.
- `invoice_pdf` - A link to download PDF of the invoice if finalised. Available in the invoice events: Invoice created, Invoice upcoming, Invoice paid, Invoice payment successful, Invoice payment failed, Invoice voided, Invoice marked uncollectible.
- `invoice_lines` - An array of invoice lines. Each item will have, `description` , `quantity`, `amount` and `currency`. Available in the invoice events: Invoice created, Invoice upcoming, Invoice paid, Invoice deleted, Invoice payment successful, Invoice payment failed, Invoice voided, Invoice marked uncollectible.
- `total` - Total amount on invoice, including tax. Available in all invoice payment and checkout session expired events.
- `subtotal` - Total amount on invoice before tax is applied. Available in all invoice payment and checkout session expired events.
- `amount_paid` - Amount paid on the invoice. Available in all invoice payment events. 
- `amount_due` - Amount due to be paid on invoice. Note that this may be less than `total` as there may be credit on the customer profile. Available in all invoice payment events. 
- `amount` - Payment amount. Available in the charge events: Charge successful and Charge failed. 
- `receipt_number` - The receipt number for a payment. Available in Chage successful, Invoice paid and Invoice successfully paid events. 
- `receipt_url` - A URL to view the payment receipt. Available in Chage successful, Invoice paid and Invoice successfully paid events. 
- `description` - Description of a failed charge. Available in failed charge events. 
- `code` - Code for a failure charge. Available in failed charge event. 
- `trial_end` - Date trial ends. Available in trial-will-end event.
- `trial_start` - Date trial starts. Available in trial-will-end event.
- `subscription_start` - Date the current subscription starts or the usage period for invoice starts. Available for customer subscription events and invoice payment events.
- `subscription_end` - Date the current subscription ends or the usage period for invoice ends. Available for customer subscription events and invoice payment events.
- `subscription_items` - An array of subscription items. Each item will have, `name` (name of plan or price), `quantity`, `amount` and `currency`.
- `currency` - Currency ISO (all caps). Available in all charge and invoice events
- `status` - Payment or subscription status of the event. For charge events, possible values are `succeeded`, `pending`, or `failed`. For subscription, possible values are `active`, `past_due`, `unpaid`, `canceled`, `incomplete`, `incomplete_expired`, or `trialing`. For invoice payments, possible values are `draft`, `open`, `paid`, `uncollectible`, or `void`
- `brand` - Card brand, e.g Visa. Available in Card will expire event.
- `exp_month` - Card expiry month. Available in Card will expire event.
- `exp_year` - Card expiry year. Available in Card will expire event.
- `last4` - Last 4 digits of card. Available in Card will expire event.
- `checkout_url` - Link to complete a checkout process. Available in checkout session expired event.

### Attribute Data

We collect the standard attributes first_name, last_name, email and number. The other attributes are prefixed with stripe_ so that it’s clear they are from Stripe. 
Note: To use as personalization tags, prefix with `meta.` e.g `meta.stripe_address_country`.

- `stripe_delinquent` 
- `stripe_address_city`
- `stripe_address_country`
- `stripe_address_line1`
- `stripe_address_line2`
- `stripe_address_state`
- `stripe_address_postal_code`

## Using event data for personalization tags
If an automation trigger is “Event is triggered” and the event type is a Stripe event, you can use any of the Stripe event data as personalization tag within messages in the automation. To do this, prefix with "`event.`". 

Remember, Engage’s personalization tag engine is built on [Liquid template language](https://shopify.github.io/liquid/), so you can use this to format your tags. 

Here is an example:

{% raw %}
> Your subscription has been successfully renewed. Your new billing period is  {{event.subscription_start \| date: “%a, %b %d” }} to {{event.subscription_end \| date: “%a, %b %d, %Y”}}.
> 
> Here is a summary:   
> {% for item in event.invoice_lines %}  
> {{item.description}} - ${{item.amount}}  
> {% endfor %}  
> 
> Total: ${{event.total}}  
> 
> Kindly click here to download your invoice: {{event.invoice_pdf}}  
> 
> Regards
{% endraw %}

Output:

>Your subscription has been successfully renewed. Your new billing period is  Wed, Aug 4 to Sat, Sep 4, 2021.
>
> Here is a summary:   
> 1 × Engage demo (at $0.90 / every 2 days) - $0.9
>
> Total: $0.9
>
> Kindly click here to download your invoice: https://pay.stripe.com/invoice/acct_1B../invst_K6../pdf
>
> Regards

