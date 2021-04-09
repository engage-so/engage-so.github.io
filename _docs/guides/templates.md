---
layout: docs
page: templates
title: Transactional email templates management
---

# Transactional email templates management

Templates allow you create a predefined content you can use for email later. It helps avoid having to always create the email body every time you want to send an email, especially emails that are sent frequently (transactional emails like notifications or password recovery for example). You create the template once, with variables that can be replaced and when you need to send the mail, you make an API call with the template name and parameters to replace the variables in your template.

A template will look something like this:

```text
Hi {%raw%}{{name}}{%endraw%},

Click here to confirm your subscription {%raw%}{{link}}{%endraw%}
```

To send the email, you only need to send the value for `{%raw%}{{name}}{%endraw%}` and `{%raw%}{{link}}{%endraw%}` instead of the full email body. 

Templates are supported by both [Mailgun](https://documentation.mailgun.com/en/latest/user_manual.html#templates) and [Amazon SES](https://aws.amazon.com/blogs/messaging-and-targeting/introducing-email-templates-and-bulk-sending/) and the way templates work in Engage is to connect directly to the relative service (depending on the one connected to your account) to manage your templates on the service. In other words, if you create a template on Engage, it is created on your Mailgun or Amazon SES account. To use the template, simply implement the API as applicable to the service you are using. Here is a reference to both:

- [Mailgun: Send with templates](https://documentation.mailgun.com/en/latest/user_manual.html#templates)
- [Amazon SES: SendTemplatedEmail](https://docs.aws.amazon.com/ses/latest/APIReference/API_SendTemplatedEmail.html)
