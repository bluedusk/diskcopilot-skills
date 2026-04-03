---
description: "Launch interactive cleanup dashboard in the browser"
---

Analyze disk usage and launch the interactive cleanup web UI. Use the diskcopilot skill for instructions.

1. Check if scanned: `diskcopilot-cli query info <path>`. Scan if needed.
2. Run analysis queries:
   - `diskcopilot-cli query tree <path> --depth 2 --json`
   - `diskcopilot-cli query summary <path> --json`
   - `diskcopilot-cli query dev-artifacts <path> --json`
   - `diskcopilot-cli query large-files <path> --min-size 100M --json`
3. Write a concise analysis summary to `/tmp/diskcopilot-insights.txt` covering:
   - Total size and file count
   - Top space consumers by category
   - What's safe to delete and what to keep
   - Recommended actions
4. Launch: `diskcopilot-cli serve <path> --insights-file /tmp/diskcopilot-insights.txt`
5. Tell the user: "Opened cleanup dashboard in your browser. Select items and trash them directly — everything goes to macOS Trash."

If no path argument is provided, use the home directory (~).
