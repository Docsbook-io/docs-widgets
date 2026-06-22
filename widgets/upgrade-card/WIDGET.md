---
name: upgrade-card
description: Renders an interactive plan upgrade card inline in chat with plan comparison and a CTA link. Use when the user needs to be shown upgrade options for Pro or Pro+ plans.
version: 1.0.0
category: conversion
modes:
  - user
  - admin
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docsbook
---

# Upgrade Card

The Upgrade Card widget displays a plan comparison card inline in the chat, showing the benefits of upgrading to Pro or Pro+ and providing a CTA link to start the checkout flow.

## When to use

This widget is rendered automatically by the `show_upgrade` tool when the agent detects the user needs a paid feature. It replaces the previous React-only `ChatUpgradeCard` component when the iframe flag is enabled.

## Input (seed via ui/initialize)

```json
{
  "targetPlan": "pro",
  "workspaceId": 123,
  "appUrl": "https://docsbook.io"
}
```

- `targetPlan`: `"pro"` or `"pro_plus"` — determines which plan's benefits are shown.
- `workspaceId`: optional workspace id forwarded to the checkout URL.
- `appUrl`: optional app base URL (defaults to current origin).

## postMessage protocol

- **Host → Widget**: `{ type: "ui/initialize", seed: { targetPlan, workspaceId, appUrl } }`
- **Widget → Host**: `{ type: "ui/ready" }` on load
- **Widget → Host**: `{ type: "ui/patch", patch: { dismissed: true } }` when user clicks "Maybe later"

The CTA button opens the existing checkout flow in a new tab (`?checkout=<plan>&workspaceId=<id>`).
