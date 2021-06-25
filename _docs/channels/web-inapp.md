---
layout: docs
page: webinapp
title: Web in-app message
description: The web in-app channel lets you send send messages that show up in your recipients browser.
---

# Web in-app message

The web in-app channel lets you send send messages that show up in your recipients browser. It shows up as a pop-up at the bottom right corner of the recipients' screen.

![Web in-app messaging](https://d2969mkc0xw38n.cloudfront.net/media/web-inapp.png)

## Setup

- Install the [Engage Javascript SDK](https://engage.so/docs/sdks/javascript). (If you haven't, please read about the [JS SDK](https://engage.so/docs/sdks/javascript) before you continue). The web in-app messaging feature only works for a web client so you need to use the CDN version. Simply copy and paste the code just before the closing `</body>` tag of your web page.

```js
!function(n){if(!window.Engage){window[n]=window[n]||{},window[n].queue=window[n].queue||[],window.Engage=window.Engage||{};for(var e=["init","identify","addAttribute","track"],i=0;i<e.length;i++)window.Engage[e[i]]=w(e[i]);var d=document.createElement("script");d.src="//d2969mkc0xw38n.cloudfront.net/next/engage.min.js",d.async=!0,document.head.appendChild(d)}function w(e){return function(){window[n].queue.push([e].concat([].slice.call(arguments)))}}}("engage");
```

- Next, initialise the SDK with your API key. You can find your API key in **Settings → Account** page of your dashboard.

```js
Engage.init('api_key')
```

- For in-app messaging, you only need to [identify the user](https://engage.so/docs/sdks/javascript#identifying-users) with the SDK. So you can do this:

```js
Engage.identify({
 id: 'u13345'
})
```

If it is on a page where you already [track user attributes](https://engage.so/docs/sdks/javascript#tracking-user-attributes) and [events](https://engage.so/docs/sdks/javascript#tracking-user-events-and-actions) with `Engage.track`, that's also totally fine. In-app messaging works as long as there is one of `Engage.identify` or `Engage.track` (or both) on the page.

## FAQ

**How this affect my pricing?**

Each message you send to a unique user contributes to your MTU (monthly tracked users). [See how we calculate MTU](/docs/guides/mtu).

**Can I use this on the free plan?**

Absolutely. However, remember that the free plan is limited to only 1,000 MTU. Your in-app message will also have a "powered by Engage" footer.

**When do users get the message?**

If the recipient is online, the message immediately pops up at the bottom right corner of the page. If they are not online, they see it when next they are online. By online, we mean when on any of your webpage with the Engage SDK integrated.

**How do you determine delivered and opened?**

We track "delivery" as when the message shows up on the recipients browser. We track "opened" as when the pop-up is closed.

**Any plans to track clicks?**

Not at the moment. If we get more interests for this, we will provide the option for click tracking.

**What happens if there are multiple messages sent before they come online?**

The see the oldest message first. Once they close it (it's marked as opened) and they move to a different page (or refresh the page), the see the next. And so on.
