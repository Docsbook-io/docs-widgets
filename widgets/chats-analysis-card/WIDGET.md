---
name: chats-analysis-card
description: Shows AI chat analysis for a workspace — questions readers asked, unanswered questions, and negative feedback, as a table with a daily query bar chart.
version: 1.0.0
category: analytics
modes:
  - admin
triggers:
  - show chats analysis
  - what are people asking my AI
  - show unanswered AI questions
  - AI chat analysis
  - show AI questions
keywords:
  - chats
  - analysis
  - ai questions
  - unanswered
  - negative feedback
  - analytics
discriminators:
  - chats analysis
  - unanswered questions
  - AI chat log
mcp_resource_uri: "ui://chats-analysis-card/render"
requires_plan: pro
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docs-widgets
---

# Chats Analysis Card

Displays a daily bar chart of AI queries and a table of questions readers asked the AI chat, including unanswered questions and sessions with negative feedback. Renders inside the Docsbook admin dashboard via a sandboxed iframe.

## Seed

Receives `{ workspaceId: number, range: string }` via `ui/initialize`.

## Data

Calls `analytics.ai_usage` via the `ui/callTool` bridge (no direct fetch) to load chat history and query counts. Renders a table-first MVP with an optional inline SVG bar chart.
