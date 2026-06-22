---
name: translation-mode-card
description: Choose translation mode — auto (built-in AI), manual, or external webhook pipeline.
version: 1.0.0
category: translation
modes:
  - admin
mcp_resource_uri: "ui://translation-mode-card/render"
keywords:
  - translation mode
  - auto
  - manual
  - external
  - webhook
discriminators:
  - translation mode
  - external webhook
  - manual translation
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docs-widgets
---

# Translation Mode Card

The Translation Mode Card lets admins select how translations are produced for a workspace. It receives the current mode and webhook URL via `ui/initialize` and emits `ui/patch` when the user saves a change.

## Seed

```json
{
  "translationMode": "auto",
  "externalTranslationWebhookUrl": null,
  "plan": "pro_plus"
}
```

## Patch shape

```json
{ "translationMode": "manual" }
```

or for external mode:

```json
{ "translationMode": "external", "externalTranslationWebhookUrl": "https://your-pipeline.example.com/translate" }
```
