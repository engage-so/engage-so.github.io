---
layout: docs
title: API
page: api-intro
description: The Engage API lets you interact with data and resources through REST. Learn more about the API format, authentication and resources.
---

# API Introduction

The Engage API lets you interact with data and resources through REST. The API accepts requests in JSON format, returns responses in JSON and uses standard HTTP for authentication, methods and response codes.

### Authentication

Authentication is via [HTTP Basic Authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) using your API key as username and API secret as password. You can view and manage these keys in the [settings page](https://app.engage.so/settings/account) of your account dashboard. On some endpoints, you can use just your API key (as username) and leave the secret empty. This makes it possible to call such endpoints from client-side applications. Endpoints that support this are marked with "works with username authentication".

### API Root

`https://api.engage.so/v1`

> Note that requests have to be HTTPS or it won't work.

### Versioning

The current API version is `v1`.

### Errors

Errors are returned with standard HTTP status codes. Error responses will come with additional body in the format:

```json
{"error": "More details about error"}
```

## Pagination

The API uses cursor-based pagination. Responses for list requests will come with a `next_cursor` and/or `previous_cursor` parameter. If you need to get the next page of dataset, make a request with the `next_cursor` parameter. To get the previous page of dataset, make a request with the `previous_cursor` dataset.

```json
{
  "data": [...],
  "next_cursor": "60583d4a60ad2a26042a9499"
}
```
```text
api.engage.so/v1/users?next_cursor=60583d4a60ad2a26042a9499
```

> You can only use one of `next_cursor` and `previous_cursor` in a request.

*An earlier version of the API lets you use the `id` field of the resource object to request the previous or next page of dataset by making a request with the parameters: `after_id` and `before_id` set to the id. This pagination style has now been deprecated and is not recommended.*

```json
{
  "data": [{
    "id": "60583d4a60ad2a26042a9499"
    ...
  }],
  "has_more": true
}
```
```text
api.engage.so/v1/users?after_id=60583d4a60ad2a26042a9499
```



## Resources

- [Users](/docs/api/users)
- [Lists](/docs/api/lists)

*More resources coming soon*
