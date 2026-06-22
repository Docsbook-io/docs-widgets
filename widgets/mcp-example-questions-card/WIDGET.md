---
name: mcp-example-questions-card
description: Editable list of example MCP questions — shows and manages suggested prompts that users can ask via the MCP server.
version: 1.0.0
category: mcp
modes:
  - admin
triggers:
  - example MCP questions
  - MCP prompts
  - suggested questions
  - edit prompts
mcp_resource_uri: "ui://mcp-example-questions-card/render"
keywords:
  - mcp
  - example
  - questions
  - prompts
  - suggested
discriminators:
  - example questions
  - MCP prompts
  - suggested
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docsbook
---

# MCP Example Questions Card

Displays and manages the ordered list of example questions/prompts that users can ask through the MCP server.

## What the user sees

An ordered list of editable prompts. Users can reorder, add, edit, and delete example questions. Save triggers a `ui/patch` with the updated list.

## Input (seed)

```json
{ "mcpExampleQuestions": ["How do I get started?", "What are the main features?"] }
```

On save, emits `ui/patch` with `{ "mcpExampleQuestions": [...] }`.
