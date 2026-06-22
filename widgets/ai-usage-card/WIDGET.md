---
name: ai-usage-card
description: Shows AI and translation usage for a workspace — queries used vs monthly limit with a progress bar.
version: 1.0.0
category: analytics
modes:
  - admin
triggers:
  - show AI usage
  - how many AI requests have I used
  - show my AI quota
  - how much translation quota is left
  - AI limit remaining
keywords:
  - ai usage
  - usage
  - limit
  - remaining
  - quota
  - translation
discriminators:
  - AI usage
  - monthly limit
  - usage quota
mcp_resource_uri: "ui://ai-usage-card/render"
requires_plan: null
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docs-widgets
---

# AI Usage Card

Displays AI query usage for the current month — used vs. limit with a progress bar and reset date. Also shows translation usage if available. Renders inside the Docsbook admin dashboard via a sandboxed iframe.

## Seed

Receives `{ workspaceId: number, range: string }` via `ui/initialize`.

## Data

Calls `analytics.ai_usage` via the `ui/callTool` bridge.
