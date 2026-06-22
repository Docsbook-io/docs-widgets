---
name: pending-translations-card
description: Review, approve or reject translations awaiting approval — with confirm step before reject.
version: 1.0.0
category: translation
modes:
  - admin
mcp_resource_uri: "ui://pending-translations-card/render"
keywords:
  - pending translations
  - approve
  - reject
  - review
  - translation queue
discriminators:
  - pending translations
  - approve translations
  - translation review
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docs-widgets
---

# Pending Translations Card

The Pending Translations Card lists translations in "draft" status awaiting review. It fetches data via the `list_pending_translations` tool (callTool bridge) seeded with `workspaceId`. Approve publishes a translation (`ui/callTool` → `approve_translation`); reject shows a confirm step before deleting (`ui/callTool` → `reject_translation`).

## Seed

```json
{ "workspaceId": 42, "plan": "pro" }
```

## Tools used

- `list_pending_translations` — fetches pending translations for the workspace
- `approve_translation` — approves (publishes) a single translation by id
- `reject_translation` — deletes a translation after user confirmation
