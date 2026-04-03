---
description: "Generate a disk usage report in the conversation"
---

Analyze disk usage and present a report directly in the conversation. Use the diskcopilot skill for instructions.

1. Check if scanned: `diskcopilot-cli query info <path>`. Scan if needed.
2. Run queries to build the report:
   - `diskcopilot-cli query tree <path> --depth 2 --json` — directory breakdown
   - `diskcopilot-cli query summary <path> --json` — cleanup summary
   - `diskcopilot-cli query dev-artifacts <path> --json` — dev artifacts
3. Present the report with:
   - Top-level directory breakdown with sizes
   - Cleanup opportunities by category (dev artifacts, large files, old files)
   - Total potential savings
   - Recommended actions

If no path argument is provided, use the home directory (~).
