---
layout: docs
title: API - Users
page: api-users
description: The User Resource allows you interact with your users on Engage.
---
# Users

The User Resource allows you interact with your users on Engage.

- [The user object](#the-user-object)
- [Create a User](#create-a-user)
- [Retrieve a User](#retrieve-a-user)
- [Update User attributes](#update-user-attributes)
- [Add User events](#add-user-events)
- [List Users](#list-users)
- [Delete User](#delete-user)

## The User object

```json
{
  "id": "5fc6477241fcec31a9548e98",
  "uid": "a.jinadu@somecorp.email",
  "uid_updateable": true,
  "first_name": "Akinyele",
  "last_name": "Jinadu",
  "number": null,
  "email": "a.jinadu@somecorp.email",
  "devices": [],
  "lists": [],
  "segments": [],
  "meta": {
    "plan": "pro",
    "age": 34
  },
  "created_at": "2021-01-12T05:24:39.062+00:00"
}
```

- `id` - A unique internal identifier for the user object.
- `uid` - The user's unique identifier in your application. If an id wasn't attached to the user data at creation (if the user was created through an integration for example), there will be an additional `uid_updateable` field with value `true`. This means you can make an update request to update the `uid`. Otherwise you cannot update the `uid`.
- `first_name` - The user's first name if added.
- `last_name` - The user's last name if added.
- `number` - The user's number if added.
- `email` - The user's email.
- `devices` - An array of object with the properties `token` and `platform` containing the user's last 5 device tokens and platform (`android` or `ios`) if synced.
- `lists` - An array of object with the properties `id` and `subscribed` containing the id and subscription status of [lists](/docs/guides/lists) the user belongs to.
- `segments` - An array of object with the properties `id` and `suppressed` containing the id and suppression status of [segments](/docs/guides/segments) the user belongs to. Suppressed mean the user has unsubscribed from a broadcast sent to this segment and will no longer get new broadcasts.
- `created_at` - Date created if exists.
- `meta` - Additional attributes attached to the user will be available as properties under meta.

## Create a User

Adds a new user to your Engage account. Use this to sync customer data with Engage when a customer signs up on your application.

Works with username authentication.

```
POST /users
```

Parameters:
- `id` - Required. An identifier for the user in your application. You can subsequently use this to update or retrieve the user. Can only contain alhabets and numbers.
- `lists` - Optional. An array of ids of lists you want to subscribe the user to. Opt-in confirmations are not sent for these even if enabled for the lists.
- `first_name` - Optional. The user's first name
- `last_name` - Optional. The user's last name
- `device_token` - Optional. The user's device token
- `device_platform` - Optional. The device platform. Supported values are `android` or `ios`
- `number` - Optional. The user's phone number in international format
- `email` - Optional. The user's email
- `created_at` - Optional. Date the user signed up on your application. Should be a valid date string.
- `meta` - Optional. An object that can contain additional user attributes. The values can be a string, number or boolean.

Example request data:
```json
{
  "id": "u144",
  "first_name": "Akinyele",
  "last_name": "Jinadu",
  "email": "a.jinadu@somecorp.email",
  "meta": {
    "plan": "pro",
    "age": 34
  },
  "created_at": "2021-01-12T05:24:39.062+00:00"
}
```

The method returns the user object. If there is an error with any of the parameters, it will return a 400 HTTP status code with details in an error object.

## Retrieve a User

```
GET /users/{uid}
```

The method returns the user object.


## Update User attributes

Update user data and attributes. Use this to update user data changes like change in plan, name, location, etc on Engage. If the user doesn't exist, this method creates the user. If the user does not have an id attached before (i.e, if `uid_updateable` is true), the request `uid` is set as the new id.

Works with username authentication if not updating the user's email. Updating the user's email requires full (key and secret) authentication.

```
PUT /users/{uid}
```

Parameters can be any or more of the following:
- `first_name` - The user's first name
- `last_name` - The user's last name
- `number` - The user's phone number in international format
- `email` - The user's email. Requires both username and password authentication
- `device_token` - Optional. The user's device token
- `device_platform` - Optional. The device platform. Supported values are `android` or `ios`
- `created_at` - Date the user signed up on your application. Should be a valid date string
- `meta` - An object containing additional user attributes to add or update. Should be string, number or boolean

Example request data:
```json
{
  "meta": {
    "plan": "custom",
    "coverage": 20 
  },
  "created_at": "2021-01-12T05:24:39.062+00:00"
}
```

The method returns the updated user object. If there is an error with any of the parameters, it will return a 400 HTTP status code with details in an error object.

## Add User events

Add user events to Engage. Use this to add user actions and events on your application to Engage. You can later segment your users based on these actions or events.

Works with username authentication.

```
POST /users/{uid}/events
```

Parameters:
- `event` - Required. The event title
- `value` - Optional. The event value. Can be a string, number or boolean
- `properties` - Optional. An object containing additional event properties. Property values can only be string, number or boolean
- `timestamp` - Optional. Timestamp of the event. If none provided, the current time is used.

Example request data:
```json
{
  "event": "Add to cart",
  "timestamp": "2020-05-30T09:30:10Z",
  "properties": {
    "product": "T123",
    "currency": "USD",
    "amount": 12.99
  }
}
```
Another example:
```json
{
  "event": "Paid",
  "value": 49.99
}
```

Example response:

```json
{ "status": "ok" }
```
If there is an error with any of the parameters, it will return a 400 HTTP status code with details in an error object.

## List Users

```
GET /users
```

Parameters:
- `limit` - Optional. Number of users to return. Defaults to 10. Maximum of 30.
- `next_cursor` - Optional. Pagination cursor for next dataset page.
- `previous_cursor` - Optional. Pagination cursor for previous dataset page.

Example response:
```json
{
  "data": [
    {
      "id": "5fc6477241fcec31a9548e98",
      "uid": "a.jinadu@somecorp.email",
      "uid_updateable": true,
      "first_name": "Akinyele",
      "last_name": "Jinadu",
      "number": null,
      "email": "a.jinadu@somecorp.email",
      "devices": [],
      "lists": [],
      "segments": [],
      "meta": {
        "plan": "pro",
        "age": 34
      },
      "created_at": "2021-01-12T05:24:39.062+00:00"
    }
  ],
  "next_cursor": "5fc6477241fcec31a9548e98"
```
Remember, you can only use one of `next_cursor` and `previous_cursor`. See [pagination](/docs/api/#pagination) for more.

## Delete User

```
DELETE /users/{uid}
```
This deletes all the user data.

Example response:
```json
{
  "status": "ok"
}
```
