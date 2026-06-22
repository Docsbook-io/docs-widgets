---
name: analytics-card
description: Shows live docs analytics for a workspace — visitors, page views, top pages and referrers, with an inline SVG line chart.
version: 1.0.0
category: analytics
modes:
  - admin
triggers:
  - show my analytics
  - how many visitors do I have
  - what are my top pages
  - show traffic
  - page views
keywords:
  - analytics
  - visitors
  - page views
  - traffic
  - top pages
  - referrers
discriminators:
  - analytics overview
  - visitor count
  - page views
mcp_resource_uri: "ui://analytics-card/render"
requires_plan: null
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docs-widgets
---

# Analytics Card

Displays live documentation analytics — total visitors, page views, a visitor line chart, top pages table, and referrers table. Renders inside the Docsbook admin dashboard via a sandboxed iframe.

## Seed

Receives `{ workspaceId: number, range: string }` via `ui/initialize`.

## Data

Calls `analytics.docs` and `analytics.feedback` via the `ui/callTool` bridge with the workspaceId and days derived from range.
