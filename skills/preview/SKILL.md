---
name: echoui-preview
description: Open a published Echo UI page in the browser for viewing or preview.
version: 1.0.0
metadata: {"openclaw":{"requires":{"env":["ECHOUI_API_KEY"]},"primaryEnv":"ECHOUI_API_KEY","emoji":"👁️"}}
---

# Echo UI Preview

## Overview

Opens a published Echo UI page URL in the user's default browser.

## Steps

1. If the user hasn't specified which file, use `echoui-list` first to show available files and their URLs.
2. Get the URL from the list response or from a previous `echoui-publish` result.
3. Open in the default browser:

```bash
if command -v open >/dev/null 2>&1; then
    open "<url>"
elif command -v xdg-open >/dev/null 2>&1; then
    xdg-open "<url>"
else
    echo "Could not detect browser opener. Visit: <url>"
fi
```

4. Tell the user the URL that was opened.
