---
name: source-of-truth-card
description: Admin card widget for the Source of Truth setting — shows the install command and a toggle to enable the graph index. Posts ui/patch back when the enabled state changes.
version: 1.0.0
category: forms
modes:
  - admin
triggers:
  - source of truth card
  - index docs graph
  - enable source of truth
  - docs graph card
mcp_resource_uri: "ui://source-of-truth-card/render"
keywords:
  - admin
  - source of truth
  - graph
  - index
  - reindex
discriminators:
  - source-of-truth-card
  - admin source of truth
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docsbook
---

# Source of Truth Card Widget

Admin card widget for the Docsbook workspace Source of Truth (graph index) setting.

## Protocol

The host sends a `ui/initialize` postMessage with a `seed` object:

```json
{
  "enabled": false
}
```

On save the widget posts back:

```json
{ "type": "ui/patch", "patch": { "sourceOfTruthEnabled": true } }
```

## Behavior

- Shows install instructions for the docs-sync Claude plugin.
- Provides a toggle to enable/disable the Source of Truth graph index.
- Save button activates when the toggle state has changed.
