---
name: openapi-renderer
description: Renders an interactive OpenAPI/Swagger API reference UI inline in the chat. Use when the user asks to view, explore, or test API endpoints.
version: 1.0.0
category: developer
modes:
  - user
triggers:
  - show API reference
  - render OpenAPI spec
  - display API docs
  - explore API endpoints
  - view Swagger UI
  - browse REST API
  - show endpoints
mcp_resource_uri: "ui://openapi-renderer/render"
keywords:
  - openapi
  - swagger
  - api
  - rest
  - endpoints
  - reference
  - http
  - json
discriminators:
  - OpenAPI
  - Swagger
  - API spec
  - swagger.json
  - openapi.yaml
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docs-widgets
---

# OpenAPI Renderer

The OpenAPI Renderer widget displays a fully interactive Swagger UI inline inside the documentation chat. Users can browse all API endpoints, expand request/response schemas, and execute live API calls — without leaving the conversation.

## When to use

Invoke this widget when a user asks to see, explore, or test API endpoints from the documentation. This includes requests like "show me the API", "what endpoints are available", "how do I call this API", or when the documentation references an OpenAPI/Swagger specification file. If the workspace's source documents include an `openapi.yaml`, `swagger.json`, or a URL pointing to an OpenAPI spec, prefer this widget over a plain text listing.

## Input

Pass a `specUrl` string containing a publicly accessible URL to an OpenAPI 3.x or Swagger 2.x specification file (JSON or YAML). Alternatively, pass a `spec` object with the parsed OpenAPI document directly. Example tool call result:

```json
{ "specUrl": "https://petstore.swagger.io/v2/swagger.json" }
```

or

```json
{ "spec": { "openapi": "3.0.0", "info": { "title": "My API" }, "paths": { ... } } }
```

## What the user sees

An interactive Swagger UI panel rendered inline in the chat bubble. Users can expand individual endpoints, view request parameters and response schemas, authorize with API keys, and send test requests directly from the widget. The panel is sandboxed and does not persist credentials outside the chat session.
