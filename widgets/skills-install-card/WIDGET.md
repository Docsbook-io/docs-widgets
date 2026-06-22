---
name: skills-install-card
description: Skills installation flow — shows the CLI commands to install docs-skills into Claude Code, Cursor, and other AI clients.
version: 1.0.0
category: skills
modes:
  - admin
triggers:
  - install skills
  - set up docs-skills
  - add skills to Claude Code
  - skills CLI
mcp_resource_uri: "ui://skills-install-card/render"
keywords:
  - skills
  - install
  - docs-skills
  - cli
  - setup
discriminators:
  - install skills
  - docs-skills
  - skills CLI
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docsbook
---

# Skills Install Card

Displays CLI install commands for adding docs-skills to Claude Code, Cursor, Windsurf, Codex CLI and other AI clients.

## What the user sees

A client selector with copy-able install commands for installing all skills or individual ones.

## Input (seed)

No seed required. The widget shows the static install commands for the docs-skills package.
