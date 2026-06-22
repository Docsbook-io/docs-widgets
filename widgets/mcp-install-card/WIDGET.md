---
name: mcp-install-card
description: MCP server connection setup — shows install commands and config snippets for Claude Code, Cursor, and other AI clients to connect to this workspace's MCP endpoint.
version: 1.0.0
category: mcp
modes:
  - admin
triggers:
  - install MCP server
  - connect MCP
  - set up Claude Code MCP
  - add MCP to Cursor
  - configure MCP client
mcp_resource_uri: "ui://mcp-install-card/render"
keywords:
  - mcp
  - install
  - connect
  - claude code
  - cursor
  - server
  - setup
discriminators:
  - MCP
  - install
  - connect
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docsbook
---

# MCP Install Card

Shows the install commands and configuration snippets to connect this workspace's MCP server to AI clients like Claude Code, Cursor, Windsurf, and others.

## What the user sees

A client selector with install commands/snippets. The user picks their AI client and gets the exact command or JSON to add the MCP server.

## Input (seed)

```json
{ "mcpServerUrl": "https://user.docsbook.io/repo/api/mcp/server" }
```

The `mcpServerUrl` is the workspace-scoped MCP endpoint URL. The widget renders install instructions for each supported client.
