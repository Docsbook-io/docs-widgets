---
name: preview-card
description: Renders a browser-window-style preview of a documentation site URL inline in chat. Use when the agent wants to show the user their published docs site or a preview URL.
version: 1.0.0
category: content
modes:
  - user
  - admin
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docsbook
---

# Preview Card

The Preview Card widget displays a browser-window-style preview of a URL (typically the user's published docs site) inline in the chat. It shows a styled header with the URL and attempts to embed the page in an iframe. If the target site blocks framing, it falls back to an Open-in-new-tab link.

## When to use

Use this widget when the agent wants to show the user their published docs site after a commit, or when previewing a specific documentation URL. Pass the same `siteUrl` that the `preview_updated` / `commit_docs` event emits.

## Input (seed via ui/initialize)

```json
{
  "siteUrl": "https://docsbook.io/myorg/myrepo",
  "previewUrl": "https://docsbook.io/myorg/myrepo"
}
```

Both `siteUrl` and `previewUrl` are accepted (whichever is present). The widget tries them in order: `siteUrl` → `previewUrl` → `url`.

## postMessage protocol

- **Host → Widget**: `{ type: "ui/initialize", seed: { siteUrl, previewUrl? } }`
- **Widget → Host**: `{ type: "ui/ready" }` on load

The widget does not POST any answer or patch back to the host — it is display-only.
