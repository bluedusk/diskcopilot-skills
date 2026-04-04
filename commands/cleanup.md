---
description: "Analyze disk usage and clean up junk files"
---

Analyze disk usage and help the user clean up. Use the diskcopilot skill for instructions.

1. Ensure diskcopilot-cli is installed (see diskcopilot skill)
2. Check if scanned: `diskcopilot-cli query info ~`. Scan if needed.
3. Run the full Disk Health Report flow from the skill (gather data, present report)
4. Ask the user what they want to clean up
5. Delete confirmed items with `diskcopilot-cli delete <path> --trash`

If no path argument is provided, use the home directory (~).
