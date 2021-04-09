---
layout: docs
title: API
page: api-intro
---

# API Introduction

The Engage API lets you interact with data and resources through REST. The API accepts requests in JSON format, returns responses in JSON and uses standard HTTP for authentication, methods and response codes.

### Authentication

Authentication is via [HTTP Basic Authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) using your API key as username and API secret as password. You can view and manage these keys in the [settings page](https://app.engage.so/settings/account) of your account dashboard. On some endpoints, you can use just your API key (as username) and leave the secret empty. This makes it possible to call such endpoints from client-side applications. Endpoints that support this are marked with "works with username authentication".

### Versioning

The current API version is `v1`.

### API Root

`api.engage.so/v1`

### Errors

Errors are returned with standard HTTP status codes. Error responses will come with additional body in the format:

```json
{"error": "More details about error"}
```

## Pagination

The API uses cursor-based pagination. This means that for endpoints that require pagination, you can use the `id` available in each item object as a pointer to get datasets before or after the id. To get the dataset before the specified id, make a request with a `before_id` parameter set to the id. To get the dataset after the specified id, use `after_id`. You can only use one of `before_id` and `after_if` in a request.

These endpoints also return a `has_more` value that is either `true` or `false`. `true` means there are more datasets that can be requested. `false` means otherwise. If none of `after_id` or `before_id` parameter is passed, `true` will mean that, there are more datasets after the last item in the returned dataset. Same with if `after_id` is passed. If `before_id` is passed, `true` will mean that there are more datasets **before** the first item in the returned dataset.

## Resources

- [Users](/docs/api/users)

*More resources coming soon*
