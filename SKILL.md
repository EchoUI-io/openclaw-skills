---
name: echoui
description: Publish HTML, CSS, JS, SVG, and image files to live Echo UI URLs. Manage published files with list, delete, and preview commands.
version: 1.0.0
metadata: {"openclaw":{"requires":{"env":["ECHOUI_API_KEY"],"bins":["curl","jq"]},"primaryEnv":"ECHOUI_API_KEY","emoji":"📡","homepage":"https://echoui.app"}}
---

# Echo UI for OpenClaw

Publish web files to live URLs with [Echo UI](https://echoui.app).

## Setup

1. Get your API key from [echoui.app/settings/api-key](https://echoui.app/settings/api-key)
2. Export it: `export ECHOUI_API_KEY="echo_live_your_key_here"`

## Skills

- **echoui-publish** — Upload HTML, CSS, JS, SVG, and image files to live URLs
- **echoui-list** — List your published files
- **echoui-delete** — Delete a published file
- **echoui-preview** — Open a published page in the browser

## Supported File Types

| Type | Extensions | Upload method |
|------|-----------|---------------|
| Text | .html, .css, .js, .svg | Raw content via JSON |
| Binary | .png, .jpg, .jpeg, .gif, .webp, .ico | Base64-encoded |
