---
name: echoui-publish
description: Upload HTML, CSS, JS, SVG, and image files to live Echo UI URLs. Use when the user wants to publish, upload, or deploy web files to a live URL.
version: 1.0.0
metadata: {"openclaw":{"requires":{"env":["ECHOUI_API_KEY"],"bins":["curl","jq"]},"primaryEnv":"ECHOUI_API_KEY","emoji":"🚀"}}
---

# Echo UI Publish

## Overview

Writes a file locally, then uploads it to Echo UI via the REST API to get a live URL.

## Quick Reference

| Extension | Type | Script |
|-----------|------|--------|
| `.html`, `.css`, `.js`, `.svg` | Text | `scripts/upload.sh` |
| `.png`, `.jpg`, `.jpeg`, `.gif`, `.webp`, `.ico` | Binary | `scripts/upload_binary.sh` |

## Script Path Resolution

Scripts are located relative to this skill file. From the skill base directory, go up two levels to the package root, then into `scripts/`:

- Upload script: `<base_directory>/../../scripts/upload.sh`
- Binary upload script: `<base_directory>/../../scripts/upload_binary.sh`

## Steps

1. Write the file content to `echoui-output/<remote_path>` locally
2. Upload using the appropriate script based on file type:

```bash
# Text files (.html, .css, .js, .svg)
bash "<resolved_scripts_dir>/upload.sh" "echoui-output/<remote_path>" "<remote_path>"

# Binary files (.png, .jpg, .jpeg, .gif, .webp, .ico)
bash "<resolved_scripts_dir>/upload_binary.sh" "echoui-output/<remote_path>" "<remote_path>"
```

3. Parse the JSON response — it returns `url`, `path`, and `size`
4. Report the live URL to the user

## Error Handling

- **401**: API key invalid or expired. Tell user to regenerate at their Echo UI dashboard.
- **422**: Validation error (unsupported extension, invalid path). Check the error message.
- **curl failure**: Check network. Default API URL is `https://echoui.app` (override with `ECHOUI_API_URL`).
