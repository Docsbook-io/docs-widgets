---
name: system-prompt-card
description: Admin card widget for editing the AI chat system prompt. Renders a textarea for the custom system prompt with a static variable-substitution hint. Posts ui/patch back to the admin host on save.
version: 1.0.0
category: forms
modes:
  - admin
triggers:
  - edit system prompt
  - ai chat persona
  - custom system prompt card
  - ai instructions card
mcp_resource_uri: "ui://system-prompt-card/render"
keywords:
  - admin
  - system prompt
  - ai chat
  - persona
  - instructions
discriminators:
  - system-prompt-card
  - admin system prompt
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docsbook
---

# System Prompt Card Widget

Admin card widget for the Docsbook workspace AI chat system prompt setting.

## Protocol

The host sends a `ui/initialize` postMessage with a `seed` object:

```json
{
  "systemPrompt": "You are a helpful assistant...",
  "isPremium": true
}
```

On save the widget posts back:

```json
{ "type": "ui/patch", "patch": { "aiChatSystemPrompt": "new prompt text" } }
```

## Behavior

- Renders a textarea with the current system prompt value.
- Shows a static hint about variable substitution (e.g. `{{title}}`, `{{url}}`).
- Save is enabled only when the value has changed from the initial seed.
- Only patches if the value changed.
