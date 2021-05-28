---
layout: docs
title: API - Lists
page: api-lists
---

# Lists

- [The list Object](#the-list-object)
- [Create a List](#create-a-list)
- [Get All Lists](#get-all-list-data)
- [Update a List](#update-a-list)
- [Archive a List](#archive-a-list)
- [Subscribe to a List](#subscribe-to-a-list)
- [Update subscriber Status](#update-subscriber-status)
- [Unsubscribe from a list ](#unsubscribe-from-a-list)


## The Lists object

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

- `id` - A unique internal identifier for the list object
- `title` - List title. 64 characters max
- `description` - The list description. Subscribers will see this. Maximum of 255 characters
- `subscriber_count` - Number of subscribers in this list. Includes pending confirmations.
- `broadcast_count` - Number of broadcasts that has been sent to this list
- `double_optin` - True, if to send a confirmation mail to subscribers for approval/permission
- `redirect_url` - URL to redirect users to after subscription. Does not apply to subscription via the API
- `created_at` - List creation date if exists

## Create a list

Adds a new list to your Engage account

Works with username & password authentication.

```
POST /lists
```

Parameters:

- `title` - Required. List title.
- `description` - Optional. String attached to the object.
- `redirect_url` - Optional. URL to redirect users to after subscription.
- `double_optin` - Optional. Set True if you want subscribers to receive confirmation mail.

Example response payload

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

## Get all list data.

The method returns lists of objects on your Engage account which include `has_more`, it returns True if the current list has another page that can be fetched. 

Works with username authentication.
```
GET /lists
```

Parameters
This endpoint supported the following queries

- `limit `- Optional. Number of lists to return. Defaults to 10. Maximum of 30.
- `next_cursor` - Optional. Pagination cursor for next dataset page.
- `previous_cursor` - Optional. Pagination cursor for previous dataset page.

NB: See [pagination](/docs/api/#pagination) for more.


Example response payload
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

## Get a list by id

Retrieves the details of a list. Supply the unique identifier of the list

Works with username authentication.
```
GET /lists/{id}
```

Example response payload
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

## Update a list

If you need to update only some list details, like title, description, double_optin and redirect url, etc on Engage, you can do so using the list `id`

Works with username authentication.
```
PUT /lists/{id}
```

Parameters can be any or more of the following:
- `title` - The list title.
- `description` - The list description.
- `redirect_url` - valid URL to redirect users to after subscription.
- `double_optin` - Set to True if you want subscribers to receive confirmation mail.

Example response payload
Return updated list object.

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

## Archive a list

Archive list on Engage means new subscribers can’t be added. Existing subscribers are not affected

Works with username and password authentication.

```
DELETE /lists/{id}
```

Example response payload

```json
{ "status": "ok" }
```

## Subscribe to a list

Creates a user and subscribes to a list. If user already exists (email), user will be added to list as well. If it is known that a user already exists and the user's uid is known, the update subscriber status endpoint can be used instead.

```
POST /lists/{id}/subscribers
```

Parameters

- `first_name` - Optional. The user's first name
- `last_name` - Optional. The user's last name
- `email` - The user's email. Requires both username and password authentication
- `number` - Optional. The user's phone number in international format
- `created_at` - Optional. Creation date if exists
- `meta` - Optional. An object containing additional user attributes to add or update. Should be string, number or boolean.

Sample response payload

```json
{ "uid": "1456" }
```

## Update subscriber status

Setting this to true updates the subscriber's subscription to true. False unsubscribes the user from the list. `subscribed` - true or false.

```
PUT /lists/{id}/subscribers/{uid}
```

Example response payload

```json
{ "subscribed": false }
```

## Unsubscribe from a list

Remove subscribers from list.

```
DELETE /lists/:id/subscribers/{uid}
```

Example response payload

```json
{ "status": "ok" }
```
