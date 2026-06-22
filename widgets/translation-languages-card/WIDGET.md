---
name: translation-languages-card
description: Manage translation languages for a workspace — toggle enabled languages via patch.
version: 1.0.0
category: translation
modes:
  - admin
mcp_resource_uri: "ui://translation-languages-card/render"
keywords:
  - translation
  - languages
  - i18n
  - translate
discriminators:
  - translation languages
  - enable language
  - manage translations
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docs-widgets
---

# Translation Languages Card

The Translation Languages Card lets admins enable and disable translation languages for a workspace. It receives the current list of enabled languages via `ui/initialize` and emits `ui/patch` with the updated `enabledLanguages` array when the user saves.

## Seed

```json
{
  "enabledLanguages": ["fr", "de"],
  "plan": "pro"
}
```

## Patch shape

```json
{ "enabledLanguages": ["fr", "de", "es"] }
```
