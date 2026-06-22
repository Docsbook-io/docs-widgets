---
name: webhooks-card
description: Admin card widget for managing workspace webhooks — list, register, test, and delete webhook subscriptions with HMAC signing and delivery history.
version: 1.0.0
category: webhooks
modes:
  - admin
triggers:
  - manage webhooks
  - register a webhook
  - add webhook
  - list webhooks
  - delete webhook
  - test webhook
mcp_resource_uri: "ui://webhooks-card/render"
requires_plan: pro
keywords:
  - webhooks
  - events
  - hmac
  - delivery
  - subscriptions
discriminators:
  - webhooks-card
  - admin webhooks
built_in: true
author: Docsbook
repository: https://github.com/docsbook-io/docsbook
---

# Webhooks Card

An admin card widget for managing workspace webhook subscriptions. Lists registered webhooks grouped by event category, allows registering new webhooks with HMAC signing, testing them (shows pass/fail + HTTP status), and deleting them (with a confirmation step).

## What the user sees

- A flat list of registered webhooks grouped by category (Plan, Content, Translation, Chat, etc.)
- Each row shows the event type, endpoint URL, last delivery status, and last delivery time
- An "Add webhook" button that expands a registration form
- "Test" button per row — shows pass/fail + HTTP status (not the full response body)
- "Delete" button per row — requires a confirm click before proceeding

## callTool bridge

The widget calls four tools via the `ui/callTool` id-correlated bridge:

### list_webhooks
```json
{ "type": "ui/callTool", "id": "<uuid>", "name": "list_webhooks", "args": { "workspaceId": 123 } }
```
Returns an array of webhook subscription rows.

### register_webhook
```json
{ "type": "ui/callTool", "id": "<uuid>", "name": "register_webhook", "args": { "workspaceId": 123, "event_type": "chat_negative_feedback", "url": "https://...", "secret": "optional" } }
```
Returns `{ id, secret }` for the newly created webhook.

### test_webhook
```json
{ "type": "ui/callTool", "id": "<uuid>", "name": "test_webhook", "args": { "webhookId": 42 } }
```
Returns `{ ok, status }` — pass/fail flag and the HTTP response status code.

### delete_webhook
```json
{ "type": "ui/callTool", "id": "<uuid>", "name": "delete_webhook", "args": { "webhookId": 42 } }
```
Returns `{ ok: true }` on success.
