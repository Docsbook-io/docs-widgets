---
name: cost-analysis-card
description: Shows the AI cost/spend breakdown for a workspace — total estimated monthly cost and per-model breakdown table.
version: 1.0.0
category: analytics
modes:
  - admin
triggers:
  - show AI cost breakdown
  - how much is the AI costing me
  - show AI spend
  - AI cost analysis
  - billing breakdown
keywords:
  - cost
  - spend
  - ai cost
  - billing
  - breakdown
  - analytics
discriminators:
  - cost analysis
  - AI spend
  - billing breakdown
mcp_resource_uri: "ui://cost-analysis-card/render"
requires_plan: pro_plus
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docs-widgets
---

# Cost Analysis Card

Displays estimated AI cost breakdown for the workspace — total monthly cost and a per-model/provider table. Renders inside the Docsbook admin dashboard via a sandboxed iframe.

## Seed

Receives `{ workspaceId: number, range: string }` via `ui/initialize`.

## Data

Calls `analytics.ai_usage` via the `ui/callTool` bridge (using `costBreakdown` and `totalEstimatedCost` fields from the response).
