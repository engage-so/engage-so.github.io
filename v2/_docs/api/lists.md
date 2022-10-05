---
layout: docs
title: API - Lists
page: api-lists
description: The List Resource allows you interact with your user lists on Engage.
---

# Lists

The List Resource allows you interact with your user lists on Engage. You can [learn more about lists here](/docs/guides/lists).

- [The List Object](#the-list-object)
- [Create a List](#create-a-list)
- [Get All Lists](#get-all-list)
- [Update a List](#update-a-list)
- [Archive a List](#archive-a-list)
- [Subscribe to a List](#subscribe-to-a-list)
- [Update subscriber status](#update-subscriber-status)
- [Remove subscriber from List](#remove-subscriber-from-list)

## The List object

```json
{
  "id": "5fc6477241fcec31a9548e98",
  "title": "Waitlist",
  "description": "Awesome product waiting list",
  "subscriber_count": 0,
  "broadcast_count": 0,
  "double_optin": true,
  "redirect_url": "http://www.shorturl.com/home",
  "created_at": "2011-10-05T14:48:00.000Z"
}
```

- `id` - A unique internal identifier for the List object.
- `title` - List title. 64 characters max.
- `description` - The List description. Subscribers will see this. Maximum of 255 characters.
- `subscriber_count` - Number of subscribers in this List. Includes pending confirmations.
- `broadcast_count` - Number of broadcasts that has been sent to this List.
- `double_optin` - If to send a confirmation mail to subscribers for approval/permission.
- `redirect_url` - URL to redirect users to after subscription. Does not apply to subscription via the API.
- `created_at` - List creation date if exists.

## Create a List

Adds a new List to your Engage account.

Works with username & password authentication.

```
POST /lists
```

Parameters:

- `title` - Required. List title.
- `description` - Optional. String attached to the object.
- `redirect_url` - Optional. URL to redirect users to after subscription.
- `double_optin` - Optional. Set to `true` if you want subscribers to receive confirmation mail.

Example response payload:

```json
{
  "id": "60036440419768607192801b",
  "title": "Monthly subscription",
  "description": "Awesome product waiting list",
  "subscriber_count": 0,
  "broadcast_count": 0,
  "double_optin": false,
  "redirect_url": null,
  "created_at": "2011-10-05T14:48:00.000Z"
}
```

## Get all List

Get all List objects.

Works with username authentication.

```
GET /lists
```

Parameters:

- `limit` - Optional. Number of Lists to return. Defaults to 10. Maximum of 30.
- `next_cursor` - Optional. Pagination cursor for next dataset page.
- `previous_cursor` - Optional. Pagination cursor for previous dataset page.

NB: See [pagination](/docs/api/#pagination) for more.

Example response payload:

```json
{
 "data": [
    {
    "id": "5fc6477241fcec31a9548e98",
    "title": "Waitlist",
    "description": null,
    "subscriber_count": 12,
    "broadcast_count": 0,
    "double_optin": true,
    "redirect_url": null,
    "created_at": "2011-10-05T14:48:00.000Z"
    },
    {...},
    {...}
  ],
  "next_cursor": "5fc6477241fcec31a9548e98"
}
```

## Get a List by id

Get the List object.

Works with username authentication.

```
GET /lists/{id}
```

Example response payload:

```json
{
  "id": "60036440419768607192801b",
  "title": "Monthly subscription",
  "description": "Awesome product waiting list",
  "subscriber_count": 0,
  "broadcast_count": 0,
  "double_optin": false,
  "redirect_url": null,
  "created_at": "2011-10-05T14:48:00.000Z"
}
```

## Update a List

Update List object.

Works with username authentication.

```
PUT /lists/{id}
```

Parameters can be any or more of the following:

- `title` - The List title.
- `description` - The List description.
- `redirect_url` - Valid URL to redirect users to after subscription.
- `double_optin` - Set to `true` if you want subscribers to receive confirmation mail.

Example response payload (Returns updated List object):

```json
{
  "id": "60036440419768607192801b",
  "title": "Monthly subscription",
  "description": "Awesome product waiting list",
  "subscriber_count": 0,
  "broadcast_count": 0,
  "double_optin": false,
  "redirect_url": null,
  "created_at": "2011-10-05T14:48:00.000Z"
}
```

## Archive a List

Archive a List. This means new subscribers can’t be added. Existing subscribers will not be affected.

Works with username and password authentication.

```
DELETE /lists/{id}
```

Example response payload:

```json
{ "status": "ok" }
```

## Subscribe to a List

Creates a user and subscribes the user to a List. If user already exists (either by email or number), the user will be added to the List as well. If it is known that a user already exists and the user's uid is known, the update subscriber status endpoint can be used instead.

```
POST /lists/{id}/subscribers
```

Parameters:

- `first_name` - Optional. The user's first name
- `last_name` - Optional. The user's last name
- `email` - The user's email. Requires both username and password authentication.
- `number` - Optional. The user's phone number in international format/
- `created_at` - Optional. Creation date if exists.
- `meta` - Optional. An object containing additional user attributes to add or update. Should be string, number or boolean.

Sample response payload:

```json
{ "uid": "1456" }
```

## Update subscriber status

Setting this to `true` updates the subscriber's subscription to true. `false` unsubscribes the user from the List.

```
PUT /lists/{id}/subscribers/{uid}
```

Example response payload

```json
{ "subscribed": false }
```

## Remove subscriber from List

Remove subscriber from a List

```
DELETE /lists/:id/subscribers/{uid}
```

Example response payload:

```json
{ "status": "ok" }
```
