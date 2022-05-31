---
layout: docs
page: tags
title: Personalization tags
description: Personalization tags allow you customise your messages with customer or event data. Learn how to use them in your broadcasts and automation messages. 
---

# Personalization tags

Personalization tags lets you use texts in the form of `{%raw%}{{tag}}{%endraw%}` to represent user attributes and some platform attributes in your broadcast or automation content. When the broadcast is sent, the system replaces these tags with what they actually represent. If for example you create a broadcast or automation message with this content:

> Hi {%raw%}{{first_name}}{%endraw%}, welcome onboard!

and you send it to a list with 2 customers with the first names **Jane** and **Doe**, the broadcast will be sent as 

**Hi Jane, welcome onboard!** to Jane; and **Hi Doe, welcome onboard!** to Doe.

## The tags

{%raw%}
- `{{email}}` - Customer's email.
- `{{first_name}}` - Customer's first name, if added.
- `{{last_name}}` - Customer's last name, if added.
- `{{number}}` - Customer's phone number (international format), if added. 
- `{{meta.attribute}}` - Any other customer's attribute where `attribute` is the name of the attribute. e.g `{{meta.amount_paid}}`.
- `{{unsubscribe_url}}` - Broadcast or automation unsubscribe link. Only available if enabled for the broadcast or automation. By default, Engage adds an unsubscribe link at the end of unsubscribe-enabled messages. However, if your message already includes the unsubscribe_url tag, Engage will not include the unsubscribe footer.
{%endraw%}

## Personalization tags in automation messages

Depending on your automation trigger, additional personalization tags can be available for your automation messages. These tags will start with `event.`. For example, if your automation is triggered by the Stripe event **Charge successful** (`charge.succeeded`), the following additional tags are available:
- `event.amount`
- `event.receipt_number`
- `event.receipt_url`
- `event.status`

This is properly documented in the related integrations page. For example, you can see all the personalization tags available for Stripe event triggers in our [Stripe documentation page](/docs/integrations/stripe).

## Advanced

Engage's personalization tag engine system is built on [Shopify's liquid](https://shopify.github.io/liquid/). This means you can do a lot more. You can create conditional blocks, work with loops, and manipulate tags with filters. [Learn more](https://shopify.github.io/liquid/).

## Examples

Here is a simple broadcast message:

{% raw %}
> Hello {{first_name}},
>
> Your monthly summary is now available on your dashboard. Kindly login to your account to view it.
>
> {% if meta.paid_subscriber %}Remember that as a paid subscriber, you have access to the members only Slack account.{% endif %}  
> 
> Regards
{% endraw %}

Output if recipient has `paid_subscriber` attribute:

> Hello Aaron,
>
> Your monthly summary is now available on your dashboard. Kindly login to your account to view it.
>
> Remember that as a paid subscriber, you have access to the members only Slack account.
> 
> Regards

Output if recipient does not have `paid_subscriber` attribute:

> Hello Wole,
>
> Your monthly summary is now available on your dashboard. Kindly login to your account to view it.
>
> Regards

Here is an example automation message triggered by the Stripe event **Invoice payment successful** (`invoice.payment_succeeded`). Notice how the liquid filter `date` is used to format the subscription dates. Also notice the `for` loop.

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

> Your subscription has been successfully renewed. Your new billing period is  Wed, Aug 4 to Sat, Sep 4, 2021.
>
> Here is a summary:   
> 1 × Engage demo (at $0.90 / every 2 days) - $0.9
>
> Total: $0.9
>
> Kindly click here to download your invoice: https://pay.stripe.com/invoice/acct_1B../invst_K6../pdf
>
> Regards


