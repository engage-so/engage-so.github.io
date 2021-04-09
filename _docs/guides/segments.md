---
layout: docs
page: segments
title: Segmenting customers
---

# Segmenting customers

Once you have your [customer data connected](/docs/guides/connecting-user-data) to Engage, one of the things you can do is use the data to segment your customers. Creating and managing these segments can easily be done on the [Segments](https://app.engage.so/users/segments) page of the users module on the dashboard.

Segments are user groups based on customer attributes and events. When you create a segment, you add customer attributes or/and events you want and customers that match the filters are automatically added to the segment. Subsequently, when new customers are tracked or attributes or events of existing users change, they automatically join or leave the segment.

![Segments](/assets/images/docs/segments.gif)

Customer segmentation is useful for 3 things

- Tracking attribute or event changes across time. For example, you may want to know what percent of your customers **Signed up** but did not **complete their KYC** process after **3 days**.
- Sending manual broadcasts to specific category of customers. Example: Offer a discount to customers that have used their virtual card more than 5 times this month.
- Sending automated messages. Example: create an automation that automatically sends a reminder to complete KYC if hasn't been done after 3 days of sign up.

Segment subscriptions are automatically managed by Engage. This means you cannot manually add or remove a customer from a segment. They are automatically added or removed by the system based on changes to their attributes or events.

When you send a broadcast to a segment and enable unsubscribe, customers that unsubscribed will still belong to the segment but will stop getting that type of broadcast.
