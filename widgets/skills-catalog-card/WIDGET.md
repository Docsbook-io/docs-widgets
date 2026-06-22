---
name: skills-catalog-card
description: Skills catalog browser — search and browse available docs-skills. Uses the find_skill tool via callTool bridge for debounced search.
version: 1.0.0
category: skills
modes:
  - admin
triggers:
  - browse skills catalog
  - search skills
  - find a skill
  - what skills are available
mcp_resource_uri: "ui://skills-catalog-card/render"
keywords:
  - skills
  - catalog
  - browse
  - search
  - find
discriminators:
  - skills catalog
  - browse skills
  - search skills
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docsbook
---

# Skills Catalog Card

A searchable catalog of docs-skills. Users can type a query and the widget calls `find_skill` via the `ui/callTool` bridge to retrieve matching skills from the index.

## What the user sees

A search input and a grid of skill cards showing name, plan, and description. Searching debounces 300ms then calls `find_skill`. Empty query shows all skills.

## callTool bridge

```json
{ "type": "ui/callTool", "id": "<uuid>", "name": "find_skill", "args": { "query": "...", "max_results": 10 } }
```

The host responds with:
```json
{ "type": "ui/toolResult", "id": "<uuid>", "ok": true, "result": { "matches": [...] } }
```
