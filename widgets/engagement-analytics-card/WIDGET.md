---
name: engagement-analytics-card
description: Shows engagement analytics — popular searches, failed searches, negative feedback pages, and reader page journeys.
version: 1.0.0
category: analytics
modes:
  - admin
triggers:
  - show failed searches
  - what are people searching for
  - show popular searches
  - where do readers drop off
  - page journeys
  - negative feedback pages
keywords:
  - searches
  - failed searches
  - popular searches
  - journeys
  - feedback
  - engagement
  - analytics
discriminators:
  - failed searches
  - popular searches
  - page journeys
  - engagement analytics
mcp_resource_uri: "ui://engagement-analytics-card/render"
requires_plan: pro
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docs-widgets
---

# Engagement Analytics Card

Displays deeper engagement analytics — popular searches, failed searches, pages with negative feedback, and reader page journeys. Renders inside the Docsbook admin dashboard via a sandboxed iframe.

## Seed

Receives `{ workspaceId: number, range: string }` via `ui/initialize`.

## Data

Calls `analytics.popular_searches`, `analytics.failed_searches`, `analytics.negative_feedback`, and `analytics.page_journeys` via the `ui/callTool` bridge.
