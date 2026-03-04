---
name: echoui-list
description: List published files on Echo UI, check URLs, or verify a deployment.
version: 1.0.0
metadata: {"openclaw":{"requires":{"env":["ECHOUI_API_KEY"],"bins":["curl"]},"primaryEnv":"ECHOUI_API_KEY","emoji":"📋"}}
---

# Echo UI List Files

## Overview

Lists all published files for the authenticated user, with optional prefix filtering.

## Script Path Resolution

From the skill base directory, go up two levels to the package root, then into `scripts/`:

- Script path: `<base_directory>/../../scripts/list.sh`

## Steps

1. List files:

```bash
# All files
bash "<resolved_script_path>"

# Filtered by prefix
bash "<resolved_script_path>" "reports/"
```

2. Present results in a readable format showing path, URL, size, and last updated time.

## Error Handling

- **401**: API key invalid. Tell the user to regenerate it.
- **Empty array `[]`**: No files published yet. Suggest using `echoui-publish`.
