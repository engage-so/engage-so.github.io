---
layout: docs
page: tags
title: Personalization tags
---
# Personalization tags

Personailization tags lets you use texts in the form of `{%raw%}{{tag}}{%endraw%}` to represent user attributes and some platform attributes in your broadcast content. When the broadcast is sent, the system replaces these tags with what they actually represent. If for example you create a broadcast with this content

*Hi {%raw%}{{first_name}}{%endraw%}, welcome onboard!*

and you send it to a list with 2 users with the first names Jane and Doe, the broadcast will be sent as 

*Hi Jane, welcome onboard!* to Jane; and *Hi Doe, welcome onboard!* to Doe.

### The tags

{%raw%}
- `{{email}}` - User's email.
- `{{first_name}}` - User's first name, if added.
- `{{last_name}}` - User's last name, if added.
- `{{meta.attribute}}` - Any other user's attribute where `attribute` is the name of the attribute. e.g `{{meta.amount_paid}}`.
- `{{unsubscribe_url}}` - Broadcast unsubscribe link. Only available if enabled for the broadcast.
{%endraw%}

### Advanced

Engage's broadcast system is built on [Shopify's liquid](https://shopify.github.io/liquid/). This means you can do a lot more. You can create conditional blocks, work with loops, and manipulate tags with filters. [Learn more](https://shopify.github.io/liquid/).
