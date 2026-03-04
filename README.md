# Echo UI Skills for OpenClaw

Publish HTML, CSS, JS, SVG, and image files to live [Echo UI](https://echoui.app) URLs from your OpenClaw agent.

## Installation

Copy this skill package to your OpenClaw workspace:

```bash
cp -r echoui-openclaw ~/.openclaw/skills/echoui
```

Or install from ClawHub (coming soon):

```bash
clawhub install echoui
```

## Prerequisites

- An [Echo UI](https://echoui.app) account with an API key
- `curl` and `jq` installed
- `ECHOUI_API_KEY` environment variable set

### Setup

1. Get your API key from [echoui.app/settings/api-key](https://echoui.app/settings/api-key)
2. Add to your shell profile:
   ```bash
   export ECHOUI_API_KEY="echo_live_your_key_here"
   ```

## Skills

| Skill | Description |
|-------|-------------|
| `echoui-publish` | Upload files to live URLs |
| `echoui-list` | List published files |
| `echoui-delete` | Delete a published file |
| `echoui-preview` | Open a page in the browser |

## Supported File Types

| Type | Extensions | Upload method |
|------|-----------|---------------|
| Text | `.html`, `.css`, `.js`, `.svg` | Raw content via JSON |
| Binary | `.png`, `.jpg`, `.jpeg`, `.gif`, `.webp`, `.ico` | Base64-encoded |

## Configuration

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `ECHOUI_API_KEY` | Yes | — | Your Echo UI API key (starts with `echo_live_`) |
| `ECHOUI_API_URL` | No | `https://echoui.app` | Custom API URL (for self-hosted instances) |

## Structure

```
echoui-openclaw/
├── SKILL.md              # Root skill definition
├── skills/
│   ├── publish/SKILL.md  # Upload files to live URLs
│   ├── list/SKILL.md     # List published files
│   ├── delete/SKILL.md   # Delete a published file
│   └── preview/SKILL.md  # Open page in browser
└── scripts/
    ├── upload.sh          # Text file upload
    ├── upload_binary.sh   # Binary file upload (base64)
    ├── list.sh            # List files API call
    └── delete.sh          # Delete file API call
```

## License

MIT
