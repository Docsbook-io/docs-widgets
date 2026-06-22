---
name: own-api-key-card
description: Admin card widget for setting the workspace's own AI provider API key. Write-only — the widget never receives the real key. The seed carries only { masked, hasKey } metadata. Only patches aiApiKey when the user types a new value.
version: 1.0.0
category: forms
modes:
  - admin
triggers:
  - set own api key
  - bring your own key
  - ai provider key card
  - own api key card
mcp_resource_uri: "ui://own-api-key-card/render"
keywords:
  - admin
  - api key
  - own key
  - provider
  - openai
  - anthropic
discriminators:
  - own-api-key-card
  - admin api key
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docsbook
---

# Own API Key Card Widget

Admin card widget for setting a workspace's own AI provider API key.

## Security

**Write-only.** The widget NEVER receives the real key. The seed carries only:
- `masked: true` — always true, indicates write-only mode
- `hasKey: boolean` — whether a key is currently set

## Protocol

The host sends a `ui/initialize` postMessage with a `seed` object:

```json
{
  "masked": true,
  "hasKey": true
}
```

On save the widget posts back only when a new key was entered:

```json
{ "type": "ui/patch", "patch": { "aiApiKey": "sk-..." } }
```

If the field was not edited (or cleared), no patch is sent.

## Behavior

- Shows a masked input (type="password") that is always empty on load.
- When `hasKey` is true, shows a "Key is set" indicator.
- Save only sends a patch if the field contains a non-empty new value.
- Clearing the field and saving sends `{ aiApiKey: "" }` to clear the stored key.
