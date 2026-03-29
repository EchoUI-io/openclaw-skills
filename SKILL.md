---
name: echoui
description: Publish HTML, CSS, JS, SVG, images, PDFs, and other files to live Echo UI URLs. Manage published files with list, delete, and preview commands.
version: 1.1.0
metadata: {"openclaw":{"requires":{"env":["ECHOUI_API_KEY"],"bins":["curl","jq","base64"]},"primaryEnv":"ECHOUI_API_KEY","emoji":"📡","homepage":"https://echoui.app"}}
---

# Echo UI for OpenClaw

Publish files to live URLs with [Echo UI](https://echoui.app).

## Setup

1. Get your API key from [echoui.app/settings/api-key](https://echoui.app/settings/api-key)
2. Export it: `export ECHOUI_API_KEY="echo_live_your_key_here"`
3. Optional: override the API origin with `ECHOUI_API_URL` (defaults to `https://echoui.app`)

## API Contract

Use the Echo UI REST API like this:

- **Endpoint:** `POST ${ECHOUI_API_URL:-https://echoui.app}/api/v1/files`
- **Auth:** `Authorization: Bearer $ECHOUI_API_KEY`
- **Accept:** `application/json`
- **Body for text files:** `{ "content": "...", "remote_path": "path/to/file.ext" }`
- **Body for binary files:** `{ "content": "<base64>", "remote_path": "path/to/file.ext", "encoding": "base64" }`

Important:
- Do **not** use `/api/files` with `filename`; the working Echo UI plugin uses `/api/v1/files` with `remote_path`
- For HTML uploads, sending raw HTML to the wrong endpoint can trigger AWS WAF (`CrossSiteScripting_BODY`)
- Prefer mirroring the EchoUI Claude Code plugin request shape

## Skills

- **echoui-publish** — Upload HTML, CSS, JS, SVG, images, PDFs, and other files to live URLs
- **echoui-list** — List published files
- **echoui-delete** — Delete a published file
- **echoui-preview** — Open a published file in the browser

## Supported File Types

Common supported types include:

- **Text / source:** `.html`, `.css`, `.js`, `.svg`, `.txt`, `.md`, `.json`, `.xml`
- **Images / binary:** `.png`, `.jpg`, `.jpeg`, `.gif`, `.webp`, `.ico`
- **Documents / binary:** `.pdf` and other document types supported by Echo UI

Rule of thumb:
- If the file is text, upload plain text content in JSON
- If the file is binary, base64-encode it and include `"encoding": "base64"`

## Example Requests

### Text file upload

```bash
CONTENT=$(cat hello.html)
PAYLOAD=$(jq -n --arg content "$CONTENT" --arg path "hello.html" '{content: $content, remote_path: $path}')

curl -sS -X POST "${ECHOUI_API_URL:-https://echoui.app}/api/v1/files" \
  -H "Authorization: Bearer ${ECHOUI_API_KEY}" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  --data "$PAYLOAD"
```

### Binary file upload

```bash
CONTENT=$(base64 -w0 report.pdf 2>/dev/null || base64 report.pdf)
PAYLOAD=$(jq -n --arg content "$CONTENT" --arg path "report.pdf" '{content: $content, remote_path: $path, encoding: "base64"}')

curl -sS -X POST "${ECHOUI_API_URL:-https://echoui.app}/api/v1/files" \
  -H "Authorization: Bearer ${ECHOUI_API_KEY}" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  --data "$PAYLOAD"
```

### List files

```bash
curl -sS "${ECHOUI_API_URL:-https://echoui.app}/api/v1/files" \
  -H "Authorization: Bearer ${ECHOUI_API_KEY}" \
  -H "Accept: application/json"
```

## Expected Response

Successful uploads return JSON like:

```json
{"url":"https://<subdomain>.echoui.app/hello.html","path":"hello.html","size":568}
```

## Error Handling

- **401** — API key invalid or expired
- **403** — wrong endpoint, WAF block, or access policy issue
- **422** — validation error (unsupported extension, invalid path, malformed payload)
- **Non-JSON 403 HTML** — often means the request hit the wrong route or was blocked before app-level handling
