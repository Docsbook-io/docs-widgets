---
name: custom-questions-card
description: Admin card widget for editing the three suggested questions shown in the AI chat panel. Renders an ordered list of text inputs and posts ui/patch back to the admin host on save.
version: 1.0.0
category: forms
modes:
  - admin
triggers:
  - edit custom questions
  - suggested questions card
  - ai chat starter questions
  - custom questions card
mcp_resource_uri: "ui://custom-questions-card/render"
keywords:
  - admin
  - custom questions
  - suggested questions
  - ai chat
  - prompts
discriminators:
  - custom-questions-card
  - admin custom questions
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docsbook
---

# Custom Questions Card Widget

Admin card widget for the Docsbook workspace AI chat suggested questions setting.

## Protocol

The host sends a `ui/initialize` postMessage with a `seed` object:

```json
{
  "questions": ["What is X?", "How do I Y?", ""],
  "isPremium": true
}
```

On save the widget posts back:

```json
{ "type": "ui/patch", "patch": { "customQuestions": ["What is X?", "How do I Z?"] } }
```

Empty strings are filtered out. Only non-empty, trimmed questions are saved.

## Behavior

- Renders three labeled text inputs (Question 1, 2, 3).
- Save is enabled when any question has changed from the initial seed.
- Empty questions are filtered out before patching.
