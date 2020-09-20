---
layout: docs
---
# Javascript SDK

The Javascript SDK allows you to automatically identify users and capture actions and attributes on your site. It can be used both in Node.js or in the browser.

*New to Engage? Create an account*

### Installation

**NPM**
`npm install —save @engage/js`
Or 
`yarn add @engage/js`

**CDN**
Alternatively, you can simply load it from our CDN
`<script src=“//d2wy8f7a9ursnm.cloudfront.net/next/engage.min.js”></script>`

### Configuration

```js
// commonjs/node-style require
const Engage = require(‘@engage/js’)
```

```js
// ES module-style import
import Engage from ‘@engage/js’
```

Use default configuration
```js
Engage.init('api_key')
```

Additional options
```js
Engage.init(options)
```

**options**
- key
- secret: Engage identifies your application with the `key` parameter. This is enough to identify and track user actions. If however you want to do more, like update or delete user data, you need to add your `secret`. This should only be used in server side apps as your secret should be treated as a password and kept confidential.
- ~~source~~
- ~~trackPages~~
- ~~debug~~


### Identifying users

Before you can track user actions or user properties, Engage needs to know some basic information about the user–a unique id, email, name (optional) and when the user signed up on your application. (See bringing in your users for more). You only need to do this once; at user signup for example.

```js
Engage.identify({
 id: 'u13345',
 email: 'dan@mail.app',
 created_at: '2020-05-30T09:30:10Z'
})
```

*id should be a unique identifier for the user. It should be a value that will not change in your application. For example, don’t use a username as id if users can update their usernames*

The `created_at` property is optional. If not added, Engage sets it to the current timestamp. Other optional properties you can include are:

- first_name
- last_name

If you need to update any of the properties (created_at, first_name, last_name), you can call `identify` with the property set to the new value. This only works when you use the `secret` parameter to initialise the SDK. Update is not allowed for client side integration. (Remember, only use your secret key in server side integrations).

If you want to update `email`  this way, the new email should not have been “identified” with a different user id.

### Tracking user attributes

You can add attributes to users for segmentation. Allowed values for user attributes are boolean, numbers or strings.

```js
Engage.addAttributes('user_id', {
 plan: 'pro',
 promotion: true
})
```

If an attribute changes at a later date, you can use the same method to update the new value.

```js
Engage.addAttributes('user_id', {
 plan: 'premium'
})
```

### Tracking user events and actions

Events and user actions can be tracked in a couple of ways. The simplest way to do this is like this:

```js
Engage.track('user_id', 'deactivate')
```

```js
Engage.track('user_id', {
 event: 'new_badge',
 value: 'gold'
 timestamp: '2020-05-30T09:30:10Z'
})
```

`timestamp` is optional. If it is not included, Engage uses the current timestamp. If included, it must be a valid date time string.

Some actions may have additional properties instead of a single value. Here is how to track those:

```js
Engage.track('user_id', {
 event: 'add_to_cart',
 timestamp: '2020-05-30T09:30:10Z',
 properties: {
   product: 'T123',
	 currency: 'USD',
   amount: 12.99
 }
})
```

### Difference between attribute and events tracking

Attributes are attached to the user’s metadata. If an attribute changes, the new value overrides the previous value. Events are not tracked that way. If an event’s value changes, the old value is not replaced. The new value is tracked with a different timestamp. This lets you be able to segment users based on old events within a time range.

### A note on values

When tracking attributes and actions, it is important you use the right data type for better segmentation. For example, instead of using a string value of ‘$12.99’ for a price, you can use a number value so that numerical operators like equality, greater than, less than can be used on the value.

To track a date attribute, use a valid date format like `2020-05-30` or `2020-05-30T09:30:10Z`.


