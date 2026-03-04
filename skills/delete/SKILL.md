---
name: echoui-delete
description: Remove or delete a published file from Echo UI.
version: 1.0.0
metadata: {"openclaw":{"requires":{"env":["ECHOUI_API_KEY"],"bins":["curl"]},"primaryEnv":"ECHOUI_API_KEY","emoji":"🗑️"}}
---

# Echo UI Delete File

## Overview

Deletes a published file from Echo UI by its remote path. This is destructive and cannot be undone.

## Script Path Resolution

From the skill base directory, go up two levels to the package root, then into `scripts/`:

- Script path: `<base_directory>/../../scripts/delete.sh`

## Steps

1. **Confirm with the user** which file to delete. If unsure, use `echoui-list` first.
2. Delete the file:

```bash
bash "<resolved_script_path>" "<remote_path>"
```

3. Check the response — `"deleted": true` means success.

## Error Handling

- **404**: File doesn't exist. Use `echoui-list` to show what's available.
- **401**: API key invalid. Tell the user to regenerate it.
