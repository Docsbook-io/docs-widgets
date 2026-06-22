---
name: fields-form
description: Generic admin form renderer for Docsbook workspace settings cards. Renders toggle, text, and color controls from a field definition array and posts patch updates back to the admin host. Use when the admin dashboard needs to display a declarative settings card inside a sandboxed iframe.
version: 1.0.0
category: forms
modes:
  - admin
triggers:
  - render admin settings form
  - workspace settings card
  - toggle settings
  - fields form widget
  - admin card form
mcp_resource_uri: "ui://fields-form/render"
keywords:
  - admin
  - form
  - fields
  - toggle
  - settings
  - workspace
discriminators:
  - fields-form
  - admin settings
  - workspace card
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docs-widgets
---

# Fields Form Widget

The Fields Form widget is a generic admin settings form renderer for Docsbook workspace cards. It is used internally by the admin dashboard to render declarative `kind:"fields"` admin cards inside a sandboxed iframe.

## Protocol

The host sends a `ui/initialize` postMessage with a `seed` object containing:

```json
{
  "fields": [
    { "key": "myToggle", "type": "toggle", "label": "Enable feature" },
    { "key": "myText", "type": "text", "label": "Custom value", "placeholder": "Enter value" },
    { "key": "myColor", "type": "color", "label": "Accent color" }
  ],
  "values": { "myToggle": true, "myText": "hello", "myColor": "#6366f1" },
  "saveId": "my-card-id",
  "isPremium": false
}
```

On save the widget posts back:

```json
{ "type": "ui/patch", "patch": { "myToggle": false } }
```

Only changed fields are included in the patch.

## Field types

- `toggle` — a boolean on/off switch
- `text` — a single-line text input
- `color` — a color swatch + hex input

## When to use

This widget is the iframe render path for all `kind:"fields"` admin cards when `NEXT_PUBLIC_WIDGET_IFRAME_ENABLED=true`. It is not intended for direct end-user use.
