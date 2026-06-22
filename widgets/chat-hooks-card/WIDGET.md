---
name: chat-hooks-card
description: Admin card widget for configuring AI chat webhook URLs (pre-hook, post-hook, streaming). Renders an ordered list of hook URL inputs and posts ui/patch back to the admin host on save.
version: 1.0.0
category: forms
modes:
  - admin
triggers:
  - configure chat hooks
  - set chat webhook URLs
  - pre-hook post-hook streaming
  - chat hooks card
mcp_resource_uri: "ui://chat-hooks-card/render"
keywords:
  - admin
  - chat hooks
  - webhook
  - pre-hook
  - post-hook
  - streaming
discriminators:
  - chat-hooks-card
  - admin chat hooks
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docsbook
---

# Chat Hooks Card Widget

Admin card widget for the Docsbook workspace AI chat webhook hook URL settings.

## Protocol

The host sends a `ui/initialize` postMessage with a `seed` object:

```json
{
  "preHookUrl": "https://...",
  "postHookUrl": "https://...",
  "streamingWebhookUrl": "https://...",
  "isPremium": true
}
```

On save the widget posts back only the changed fields:

```json
{ "type": "ui/patch", "patch": { "aiChatPreHookUrl": "https://...", "aiChatPostHookUrl": "" } }
```

## Behavior

- Renders three labeled URL inputs: Pre-hook, Post-hook, Streaming webhook.
- Save is enabled only when at least one value has changed.
- Only changed fields are included in the patch.
- Empty string clears a hook URL.
