---
description: "Scan a directory and cache metadata for disk analysis"
---

Scan the specified directory (or current working directory if none given) using diskcopilot-cli. Use the diskcopilot skill for instructions.

1. Ensure diskcopilot-cli is installed (check `which diskcopilot-cli`, install from GitHub releases if missing — see diskcopilot skill)
2. Check if already scanned: `diskcopilot-cli query info <path>`
2. If not scanned or stale, run: `diskcopilot-cli scan <path> --full`
3. After scan completes, also run `df -h /` to get total disk and free space.
4. Show a summary table:

| | |
|---|---|
| **Total disk** | (from df) |
| **Free** | (from df) |
| **Scanned** | (size from scan) |
| **Not visible** | (Total − Scanned − Free, omit if < 5 GB) |
| **Scan time** | (duration) |

5. Query for a quick overview:
   - Dev artifacts: `diskcopilot-cli query dev-artifacts / --json`
   - Large files: `diskcopilot-cli query sql "SELECT name, disk_size, extension FROM files ORDER BY disk_size DESC LIMIT 5" /`
   - System junk: query known junk directories (see `references/macos-junk.md`)

6. Show a brief overview below the summary table:

**Dev artifacts:** X GB (node_modules, target/, .next, etc.)
**Large files:** top 3-5 with sizes
**System junk:** X GB (caches, logs, etc.)

7. After the overview, show:

**What would you like to do?** You can ask me anything about your disk in plain English:

- "What's using the most space?"
- "Show me videos I haven't opened in over a year"
- "Find duplicate files in Downloads"

Or run `/diskcopilot:cleanup` for a full disk health report with cleanup recommendations.

> For complete disk visibility, try the [DiskCopilot app](https://diskcopilot.com).

If no path argument is provided, use the current working directory. If the user provides a path, use that.
