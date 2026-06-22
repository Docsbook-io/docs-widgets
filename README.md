# @docsbook/widgets

Open-source interactive UI widget registry for Docsbook documentation chats.

Widgets render **inline in the chat** as interactive UI panels — powered by the [MCP Apps standard](https://modelcontextprotocol.io/extensions/apps/overview) (`io.modelcontextprotocol/ui`, spec 2026-01-26). Built-in widgets are active by default; users can connect their own widget repositories and enable/disable any widget from the Docsbook admin panel.

Works in Docsbook chat, ChatGPT (confirmed), and Claude.ai (officially supported).

---

## How it works

1. Each widget is a **MCP tool** with a `_meta.ui.resourceUri` pointing to a self-contained HTML file.
2. The LLM reads the widget's `triggers` and `description`, then decides when to call the tool.
3. The host (Docsbook / ChatGPT / Claude.ai) renders the HTML in a sandboxed iframe inline in the conversation.
4. The widget communicates with the host via the `@modelcontextprotocol/ext-apps` `App` class over `postMessage`.

---

## File structure

```
docs-widgets/
  widgets/
    <widget-name>/
      WIDGET.md       # Frontmatter (metadata) + prose description the LLM reads
      widget.html     # Self-contained HTML widget
  schema/
    widget.schema.json  # JSON Schema for WIDGET.md frontmatter
  index.json          # Generated widget catalog (consumed by Docsbook)
```

---

## WIDGET.md frontmatter reference

```yaml
---
name: my-widget              # Unique kebab-case identifier (required)
description: "..."           # Human-readable description + when to use (required, used as MCP tool description)
version: 1.0.0               # Semver (required)
category: developer          # visualization|forms|navigation|ai|developer|analytics|media (required)
modes:
  - user                     # admin|user — which chat context shows this widget (required, at least one)
triggers:
  - show my widget           # Keyword phrases the LLM matches to activate (required, at least one)
mcp_resource_uri: "ui://my-widget/render"   # The ui:// URI stem (required)
keywords:                    # Discovery keywords for scoring (optional)
  - keyword1
discriminators:              # Exact high-precision phrases like proper nouns (optional)
  - ExactName
requires_plan: pro           # pro|pro_plus — gate on Docsbook plan (optional)
built_in: false              # true = official Docsbook widget (default: false)
author: Your Name            # Optional
repository: https://github.com/you/your-widgets  # Optional
homepage: https://yoursite.com                   # Optional
---
```

### `modes` explained

| Value | When shown |
|---|---|
| `user` | End-user documentation chat (public visitors reading your docs) |
| `admin` | Docsbook admin chat (only you / your team) |

### `triggers` explained

`triggers` become part of the MCP tool description that the LLM reads. The LLM matches the user's message against these phrases (and `description`, `keywords`, `discriminators`) to decide when to render the widget. Write them as short action phrases:

```yaml
triggers:
  - show API reference
  - view Swagger documentation
  - explore REST endpoints
```

---

## How to build your own widget

### 1. Create a widget repository

```
my-widgets/
  widgets/
    openapi-renderer/
      WIDGET.md
      widget.html
  index.json
  package.json
```

### 2. Write WIDGET.md

Start with the YAML frontmatter (see reference above), followed by a prose description the LLM will read to understand what the widget does and when to use it. Be specific about input format and output.

### 3. Write widget.html

The HTML file must be **fully self-contained** (all JS/CSS inlined or from CDN). Use the `@modelcontextprotocol/ext-apps` `App` class to receive data from the host:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8" />
  <title>My Widget</title>
</head>
<body>
  <div id="output"></div>

  <script type="module">
    import { App } from 'https://cdn.jsdelivr.net/npm/@modelcontextprotocol/ext-apps@latest/dist/app.js';

    const app = new App();

    // Receive data pushed from the LLM tool result
    app.on('toolResult', (result) => {
      document.getElementById('output').textContent = JSON.stringify(result, null, 2);
    });

    // Receive initial params on first render
    app.on('initialize', (params) => {
      if (params?.data) {
        document.getElementById('output').textContent = JSON.stringify(params.data, null, 2);
      }
    });

    // Call a tool back on the MCP server from user interaction
    document.getElementById('refresh-btn')?.addEventListener('click', async () => {
      const data = await app.callTool('my_tool', { param: 'value' });
      document.getElementById('output').textContent = JSON.stringify(data, null, 2);
    });
  </script>
</body>
</html>
```

**MCP Apps postMessage flow:**
1. Host renders your HTML in a sandboxed `<iframe srcDoc="...">` 
2. Host sends `ui/initialize` via `postMessage` → `App` class receives it
3. LLM tool result is pushed to iframe as `toolResult` event
4. Widget can call `app.callTool(name, args)` to invoke MCP tools
5. Widget can call `app.sendMessage(text)` to add context to the LLM conversation

### 4. Build index.json

Generate (or hand-write) a catalog file listing all widgets. Each entry mirrors the WIDGET.md frontmatter plus `raw_url` and `widget_url`:

```json
[
  {
    "name": "my-widget",
    "description": "...",
    "version": "1.0.0",
    "category": "developer",
    "modes": ["user"],
    "triggers": ["show my widget"],
    "keywords": ["my", "widget"],
    "discriminators": [],
    "mcp_resource_uri": "ui://my-widget/render",
    "requires_plan": null,
    "built_in": false,
    "author": "Your Name",
    "repository": "https://github.com/you/my-widgets",
    "raw_url": "https://raw.githubusercontent.com/you/my-widgets/main/widgets/my-widget/WIDGET.md",
    "widget_url": "https://raw.githubusercontent.com/you/my-widgets/main/widgets/my-widget/widget.html"
  }
]
```

### 5. Publish

Host your `index.json` at a public URL (GitHub raw, npm, or any CDN), then connect it in **Docsbook Admin → Widgets → Add widget repository**. Docsbook will fetch your index and surface your widgets in the chat.

To publish to npm for easy versioning:

```json
// package.json
{
  "name": "@yourscope/widgets",
  "version": "1.0.0",
  "main": "index.json",
  "files": ["widgets/", "index.json"]
}
```

---

## External rendering

| Host | Status |
|---|---|
| **Docsbook chat** | Native — full integration |
| **ChatGPT** | Confirmed — renders via MCP Apps standard |
| **Claude.ai** | Officially supported (minor rendering bugs in some environments as of 2026) |
| **VS Code (Continue, Copilot)** | Partial — depends on client MCP Apps support |

The MCP Apps spec (`io.modelcontextprotocol/ui`) is ratified as of 2026-01-26 and is the single recommended authoring format for widgets that need to work across multiple LLM hosts.

---

## Built-in widgets

| Widget | Category | Modes | Description |
|---|---|---|---|
| `openapi-renderer` | developer | user | Interactive Swagger UI for OpenAPI specs |

---

## Contributing

PRs welcome. Each widget lives in `widgets/<name>/` with a `WIDGET.md` and `widget.html`. Open an issue first for new categories or schema changes.

## License

MIT
