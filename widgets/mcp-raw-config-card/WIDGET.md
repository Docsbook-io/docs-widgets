---
name: mcp-raw-config-card
description: Raw JSON MCP server config editor — shows the full JSON config block for manual MCP setup. Sensitive fields (API keys/tokens) are redacted with *** in the seed; unchanged *** values are not patched on save.
version: 1.0.0
category: mcp
modes:
  - admin
triggers:
  - raw MCP config
  - MCP JSON config
  - manual MCP setup
  - MCP configuration
mcp_resource_uri: "ui://mcp-raw-config-card/render"
keywords:
  - mcp
  - raw
  - config
  - json
  - configuration
discriminators:
  - raw config
  - MCP JSON
  - manual setup
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docsbook
---

# MCP Raw Config Card

Displays the raw JSON configuration block for connecting to the workspace MCP server. Sensitive fields (like API keys/tokens) are replaced with `***` in the seed — saving an unchanged `***` value leaves the server-side value intact.

## What the user sees

A syntax-highlighted JSON editor with Copy and Save buttons. Saving emits `ui/patch` with only the changed (non-redacted) fields.

## Input (seed)

```json
{
  "mcpServerUrl": "https://user.docsbook.io/repo/api/mcp/server",
  "mcpToken": "***"
}
```

Sensitive fields are sent as `***`. On save, `***` values in unchanged positions are excluded from the patch.
