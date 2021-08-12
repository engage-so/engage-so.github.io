---
layout: docs
page: segment
title: Segment Integration
---

# Segment

Engage integrates with [Segment](https://segment.com/) as a destination for your customer data from Segment. Segment is a leading customer data platform to collect, clean and unify customer data.

## Setup

The Segment integration is avaialable to every account on Engage. Login to your Engage dashboard, visit Settings -> Integrations and click on the connect button for Segment. This will redirect you to Segment for authorization and to select your preferred workspace and source for the connection.

![Connect Segment](/assets/images/docs/segment-connect.png)

## Testing

Once done, you can test your configuration by visiting the Destination page of your Segment workspace. You should see "**Engage Messaging**" as one of the destinations. Click on it and navigate to the "**Event Tester**" tab. Send a test **Track** or **Identify** event. 

![Test Segment connection](/assets/images/docs/segment-test.png)

Check the **Customers** page of your Engage dashboard and you will see the identified or tracked customers there. You can navigate to the customer event page to see more details about the events.

![View customer event](/assets/images/docs/view-segment-event.png)

## Advanced options

You can directly add customers from Segment to a specific [list](https://engage.so/docs/guides/lists). If you haven't, create a list on your Engage dashboard. On the list page, click the **Subscription and Settings** page to get the ID of the list. Copy it. Visit the Settings tab of the "**Engage Messaging**" destination page of your Segment dashboard. Click the **List ID** section to update it with the copied list ID. 

![Update list ID](/assets/images/docs/segment-advanced.png)

If you reset your public API key on Engage, update the new public key here as well. If not, yout Segment connection will stop working as the integration uses the API key to send data to your Engage account.

## Supported Segment calls

At the moment, Engage only supports the two Segment calls: [Identify](https://segment.com/docs/connections/spec/identify/) and [Track](https://segment.com/docs/connections/spec/track/).
