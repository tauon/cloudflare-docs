---
type: example
summary: Set a Cron Trigger for your Worker.
tags:
  - Middleware
pcx_content_type: configuration
title: Setting Cron Triggers
weight: 1001
layout: example
---

{{<tabs labels="js/sw | js/esm">}}
{{<tab label="js/sw" default="true">}}

```js
addEventListener('scheduled', event => {
  event.waitUntil(triggerEvent(event.scheduledTime));
});

async function triggerEvent(scheduledTime) {
  console.log('cron processed');
}
```
{{</tab>}}
{{<tab label="js/esm">}}

```js
export default {
	async scheduled(controller, env, ctx) {
		console.log('cron processed');
	},
};
```
{{</tab>}}
{{</tabs>}}

## Setting Cron Triggers in Wrangler

If you are deploying with Wrangler, set the cron syntax (once per hour as shown below) by adding this to your `wrangler.toml` file:

```toml
name = "worker"

# ...

[triggers]
crons = ["0 * * * *"]
```

You also can set a different Cron Trigger for each environment in your `wrangler.toml`. You need to put the `[triggers]` table under your chosen environment. For example:

```toml
[env.dev.triggers]
crons = ["0 * * * *"]
```
