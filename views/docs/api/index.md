---
layout: docs
title: API
page: api-intro
---
# API Introduction

The Engage API lets you interact with data and resources through REST. The API accepts requests in JSON format, returns responses in JSON and uses standard HTTP for authentication, methods and response codes.

### Authentication

Authentication is via [HTTP Basic Authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) using your API key as username and API secret as password. You can view and manage these keys in the [settings page](https://app.engage.so/settings/account) of your account dashboard. On some endpoints, you can use just your API key (as username) and leave the secret empty. This makes it possible to call such endpoints from client-side applications. Endpoints that support this are marked with "works with username authentication"

### Versioning

The current API version is `v1`

### API Root

`api.engage.so/v1`

### Errors

Errors are returned with standard HTTP status codes. Error responses will come with additional body in the format:

```json
{"error": "More details about error"}
```

## Resources

- [Users](/docs/api/users)

*More resources coming soon*
