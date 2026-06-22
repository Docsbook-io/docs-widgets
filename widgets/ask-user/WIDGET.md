---
name: ask-user
description: Composite interactive question widget rendered inline in chat. Renders the matching control (toggle, text, choice, confirm, toggle_with_text) based on the seed kind field. On submit it posts the answer back via postMessage so the host can resume the agent loop.
version: 1.0.0
category: interaction
modes:
  - user
  - admin
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docsbook
---

# Ask User

The Ask User widget is a composite interactive panel rendered inline in chat that replaces the React-based `AskPanel`/`AskChips` components when the iframe flag is enabled. It renders one of five control kinds based on the `kind` field in its seed, then posts the user's answer back to the host via `{ type: "ui/answer" }`.

## Supported kinds

| `kind`            | Control rendered                                |
|-------------------|-------------------------------------------------|
| `choice`          | Radio-style option list (single or multi-select) |
| `confirm`         | Yes/No option list                              |
| `toggle`          | On/off toggle switch                            |
| `text`            | Single-line text input + Apply button           |
| `toggle_with_text`| Toggle + conditionally visible text input       |

## When to use

This widget is rendered automatically by the `ask_user` tool when the agent asks the user a structured question. The host forwards the `ui/answer` answer into the existing SSE halt/resume path (the same `handleWidgetAnswer → sendMessage` flow that the React renderers use).

## Input (seed via ui/initialize)

```json
{
  "kind": "choice",
  "label": "Which framework are you using?",
  "field": "__ask_user__",
  "currentValue": null,
  "options": [
    { "label": "Next.js (recommended)", "value": "nextjs", "description": "App router with React Server Components" },
    { "label": "Vite + React", "value": "vite" }
  ],
  "multiSelect": false,
  "allowOther": true
}
```

For `toggle` and `toggle_with_text`, `currentValue` carries the current state. For `text`, `currentValue` carries the initial text. For `choice`/`confirm`, `currentValue` is ignored.

## postMessage protocol

- **Host → Widget**: `{ type: "ui/initialize", seed: WidgetSpec }`
- **Widget → Host**: `{ type: "ui/ready" }` on load
- **Widget → Host (answer)**: `{ type: "ui/answer", answer: string }` when user submits
- **Widget → Host (setting change)**: `{ type: "ui/patch", patch: { [field]: value } }` for toggle/text/toggle_with_text kinds (these patch workspace settings instead of sending an answer)

The host checks `onAnswer` vs `onSave` — for `field === "__ask_user__"` it calls `onAnswer`; otherwise `onSave`.
