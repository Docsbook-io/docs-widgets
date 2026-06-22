---
name: limits-card
description: Admin card widget for displaying workspace token budget and usage. Shows credit balance, per-category usage, and a link to upgrade. Receives budget data in the seed; no writable fields.
version: 1.0.0
category: forms
modes:
  - admin
triggers:
  - limits card
  - token budget widget
  - ai usage limits
  - credits remaining card
mcp_resource_uri: "ui://limits-card/render"
keywords:
  - admin
  - limits
  - token budget
  - credits
  - usage
  - quota
discriminators:
  - limits-card
  - admin limits
  - token budget widget
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docsbook
---

# Limits Card Widget

Admin card widget that displays workspace token budget and usage information.

## Protocol

The host sends a `ui/initialize` postMessage with a `seed` object:

```json
{
  "plan": "pro_plus",
  "creditsRemaining": 15000,
  "creditsTotal": 20000,
  "creditsUsedUsers": 3000,
  "creditsUsedAdmin": 1500,
  "creditsUsedTranslations": 500,
  "resetAt": "2026-07-01T00:00:00Z",
  "ownKey": false
}
```

This widget is read-only — it does not post any `ui/patch` messages.

## Behavior

- Displays remaining credits and a visual budget bar.
- Shows per-category usage (readers AI chat, admin, translations).
- Shows reset date for Pro+ monthly plans.
- Shows an upgrade prompt for free plans.
