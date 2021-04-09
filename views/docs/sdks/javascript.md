---
layout: docs
title: Javascript SDK
description: The Engage JavaScript SDK lets you automatically identify users and capture events, actions and attributes on your site. It can be used both in Node.js or in the browser.
page: sdk-js
---
# JavaScript SDK

The Engage JavaScript SDK lets you automatically identify users and capture events, actions and attributes on your site. It can be used both in Node.js or in the browser.

*New to Engage? [Create an account](https://engage.so/).*

## Installation

```js
// NPM
npm install —save @engage_so/js
// Or Yarn
yarn add @engage_so/js
```

Alternatively, you can use directly from the CDN

```html
<script src="//d2969mkc0xw38n.cloudfront.net/next/engage.min.js"></script>
```

If you are using the CDN version, then use the code below to ensure calls to the SDK before the script is completely loaded are handled.

```js
(function(k) {
  if (window['Engage']) { return }
  window[k] = window[k] || {};
  window[k].queue = window[k].queue || [];
  window['Engage'] = window['Engage'] || {};
  function q(f) {
    return function(){
      window[k].queue.push([f].concat([].slice.call(arguments)));
    }
  }
  var options = ['init', 'identify', 'addAttribute', 'track'];
  for (var i = 0; i < options.length; i++) {
    window['Engage'][options[i]] = q(options[i]);
  }
  var el = document.createElement('script');
  el.src = '//d2969mkc0xw38n.cloudfront.net/next/engage.min.js';
  el.async = true;
  document.head.appendChild(el);
})('engage');
```

## Configuration

```js
// commonjs/node-style require
const Engage = require(‘@engage_so/js’)
```

```js
// ES module-style import
import Engage from ‘@engage_so/js’
```

Initializing the SDK with your just API key:
```js
Engage.init('api_key')
```

Initializing with additional options:
```js
Engage.init({
  key: 'api_key',
  secret: 'api_secret'
})
```

**options:**

- `key`: Your account API key. Available in your account dashboard.
- `secret`: Your account secret key. Available in your account dashboard. 

Engage identifies your application with the `key` parameter. This is enough to identify and track user events or actions. If however you want to do more, like update or delete user data, you need to add your `secret`. This should only be used in server side applications as your secret should be treated as a password and kept confidential.


## Identifying users

Before you can track user events, actions or user properties, Engage needs to know some basic information about the user–a unique id, email, name (optional) and when the user signed up on your application. ([See connecting user data](/docs/connecting-user-data) for more). You only need to do this once; at user signup for example.

```js
Engage.identify({
 id: 'u13345',
 email: 'dan@mail.app',
 created_at: '2020-05-30T09:30:10Z'
})
```

`id` should be a unique identifier for the user. It should be a value that will not change in your application. For example, don’t use a username as `id` if users can update their usernames*

The `created_at` property is optional. If not added, Engage sets it to the current timestamp. The other properties can be any parameter related to the user, e.g location, gender, plan. Here is a list of the ones we use internally; we call them standard properties:

- `first_name`
- `last_name`
- `email`
- `number`
- `device_token`
- `device_platform` (android or ios)

If you need to update any of the properties, you can call `identify` with the property set to the new value. If you want to update `email` this way, the new email should not have been "identified" with a different user id. Email update also only works when you use the `secret` parameter to initialise the SDK. Update is not allowed for client side integration. (Remember, only use your secret key in server side integrations).

> `number` must include international dialing code without the +. Valid examples are 15555551234 and 2348166877840

## Tracking user attributes

You can add attributes to users for segmentation. Allowed values for user attributes are boolean, numbers or strings. The first argument of the method is the user's id. In the examples below, we are assuming the user's id is `u144`.

```js
Engage.addAttributes('u144', {
 plan: 'pro',
 promotion: true
})
```

If an attribute changes at a later date, you can use the same method to update the new value.

```js
Engage.addAttributes('u144', {
 plan: 'premium'
})
```

## Tracking user events and actions

Events and user actions can be tracked in a couple of ways. The simplest way to do this, where `u144` is ther user's id, is like this:

```js
Engage.track('u144', 'deactivate')
```

```js
Engage.track('u144', {
 event: 'New badge',
 value: 'gold'
 timestamp: '2020-05-30T09:30:10Z'
})
```

`timestamp` is optional. If it is not included, Engage uses the current timestamp. If included, it must be a valid date time string.

Some events may have additional properties instead of a single value. Here is how to track those:

```js
Engage.track('u144', {
 event: 'Add to cart',
 timestamp: '2020-05-30T09:30:10Z',
 properties: {
   product: 'T123',
   currency: 'USD',
   amount: 12.99
 }
})
```

## Difference between attribute and events tracking

Attributes are attached to the user’s metadata. If an attribute changes, the new value overrides the previous value. Events are not tracked that way. If an event’s value changes, the old value is not replaced. The new value is tracked with a different timestamp. This lets you be able to segment users based on old events within a time range.

## A note on values

When tracking attributes and events, it is important you use the right data type for better segmentation. For example, instead of using a string value of `$12.99` for a price, you can use a number value so that numerical operators like equality, greater than, less than can be used on the value.

To track a date attribute, use a valid date format like `2020-05-30` or `2020-05-30T09:30:10Z`.


