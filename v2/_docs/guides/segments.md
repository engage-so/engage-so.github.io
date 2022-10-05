---
layout: docs
page: segments
title: Customer Segments
description: A segment is a group of your customers that share similar characteristics. Learn how to create customer segments, send targeted campaigns and create message automation with Segments.
---

# Customer Segments

Once you have your [customer data connected](/docs/guides/connecting-user-data) to Engage, you can then use the data to segment your customers.

A segment is a group of customers that share similar characteristics. This characteristics is based off the customer data – attributes and events. For example, if you track the customer attributes **location** and **plan**, you can create the segment "**Customers in city Y**" or "**Customers in a Pro plan**" or a segment that combines both attributes – **Customers on Pro plan in City Y**. Other examples are "**Customers that have not logged in in 30 days**", "**Customers that spent over $1,000 this month**".
## Use of Segments

Customer segmentation is useful for 3 things:

- Tracking changes to customer data and events across time. For example, you may want to know what percent of your customers **Signed up** but did not **complete their KYC** process after **3 days**.
- Sending manual broadcasts to specific group of customers. Example: Offer a discount to customers that have used their virtual card more than 5 times this month.
- Sending automated messages. Example: create an automation that automatically sends a reminder to complete KYC if hasn't been done after 3 days of sign up. (See [Automations](/docs/guides/automations) for more).

## Creating Segments

Creating and managing segments can be done on the [Segments](https://app.engage.so/users/segments) page on the dashboard. Navigate to **Segments** &raquo; Click the **Create a new Segment** button. Every account comes with a default segment called **All** that includes all your customers.

![Create a segment](/assets/images/docs/segments-3.png)
## Segment management is automatic

When you create a segment, you add customer attributes or/and events you want and customers that match the filters are automatically added to the segment. Subsequently, when new customers are tracked or attributes or events of existing customers change, they automatically join or leave the segment. Engage takes care of this automatically. What this also means is that you cannot manually add or remove a customer from a segment. They are automatically added or removed by the system based on changes to their attributes or events.

## Sending broadcasts to Segments

Once you have created your segment, you can send a broadcast to the segment. To send a broadcast, click on **Broadcast** in the navigation sidebar, then click on the **Create Broadcast** button. Select the channel you want to send your message through. We support the following broadcast channel – web, email, push notifications and in-app message on browser. 

![Create new broadcast](/assets/images/docs/segments-2.png)

In the broadcast message creation steps, you will see a dropdown to select **Segments/Lists you are sending to**.

![Select segment](/assets/images/docs/segments-1.png)

> When you send an email broadcast to a segment and enable unsubscribe, customers that unsubscribed will still belong to the segment but will stop getting that any email broadcast to the segment. You can override this behaviour by enabling the **Send to unsubscribed recipients** option.

## Creating automations with Segments

You can automatically send customers messages that are triggered by joining or leaving a segment. This is particularly useful for re-engagement campaigns. If for example you have created a segment of customers that have not logged in in 20 days, you can send an automated message to nudge them back as soon as they join the segment. We call this automated messaging [Automations](/docs/guides/automations).

To create an automation triggered by joining or leaving a segment, click on **Automations** in the navigation sidebar. Add an automation title. Click the **Start** button to add your automation trigger. Select the type of segment trigger (**Joins a segment** or **Leaves a segment**) and select your segment from the dropdown option.

![Create automation](/assets/images/docs/segments-4.png)
