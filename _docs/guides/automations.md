---
layout: docs
page: automations
title: Automations
---

# Automations

What's better than being able to send broadcasts to customer segments and lists is creating messages that can be automatically sent based on data driven triggers. For example, automatically send a renewal reminder mail for upcoming subscription renewal.

Automations are useful for a lot of things. You can use them for simple automated messaging like welcome emails to more complex workflows for proper customer onboarding. Here is an example:

- On new profile, send a welcome message
- If customer is yet to activate their card
- Send them an email asking if there is a way to help
- Wait for 4 more days
- If card still not activated, send another nudge

![Automations](/assets/images/docs/automations.gif)

With automations, you can easily upsell or move customers to the next phase of the growth cycle, whether that is acquisition to activation or activation to retention. This is what we mean when we say we are messaging for customer growth and retention.

### Supported triggers

A trigger is an event that causes the automation to start.

- Condition - Create a custom trigger based on customer attributes and/or events, e.g Signup date is more than 3 days ago and data usage is 0
- New profile - When a new customer data is added to your account
- User joins segment
- User joins list
- User leaves segment
- User leaves list
- User unsubscribes from segment
- User unsubscribes list

### Actions

Here are the currently supported actions:

- Send user an email
- Send user SMS
- Send user push notification
- Add user to list
- Unsubscribe user from list
- Remove user from list
- Archive user
- Add/update user's attributes
- Delete user attributes
- End automation

### Controls

- Delay - Pause automation for a specific period of time
- If/Else - Add a condition that splits the automation to a Yes or No workflow
