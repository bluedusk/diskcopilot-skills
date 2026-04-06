# diskcopilot

[![Version](https://img.shields.io/badge/version-0.5.0-blue)](https://github.com/diskcopilot/diskcopilot-skills/releases)

AI agent plugin for disk scanning, analysis, and cleanup. Requires macOS.

Teaches AI agents how to use [diskcopilot-cli](https://github.com/diskcopilot/diskcopilot-cli) — a fast disk scanner (~12s for a home directory) that caches filesystem metadata in SQLite, letting the agent write SQL to answer any disk space question.

Ask your agent things like:
- "What's taking up space on my Mac?"
- "How big are my node_modules?"
- "Help me free up 10GB"

## Install

### Claude Code

```bash
claude plugin marketplace add diskcopilot/diskcopilot-skills
claude plugin install diskcopilot
```

The plugin will automatically install the `diskcopilot-cli` binary on first use.

### Other agents (Cursor, Copilot, Codex, Windsurf, Gemini CLI)

One-line install — works with any agent that supports the [Agent Skills](https://agentskills.io) standard:

```bash
mkdir -p ~/.agents/skills/diskcopilot && curl -fsSL https://raw.githubusercontent.com/diskcopilot/diskcopilot-skills/main/skills/diskcopilot/SKILL.md -o ~/.agents/skills/diskcopilot/SKILL.md
```

The skill includes auto-install instructions for the CLI binary — no manual setup needed.

## Commands

| Command | What it does |
|---------|-------------|
| `/diskcopilot:scan` | Scan a directory (or cwd) and cache metadata |
| `/diskcopilot:cleanup` | Analyze + open browser dashboard to select and trash items |
| `/diskcopilot:report` | Analyze + show report in conversation |

## Privacy

`diskcopilot-cli` only reads filesystem metadata (names, sizes, timestamps). It has no network dependencies and never sends data anywhere. The interactive cleanup UI runs on localhost with a per-session auth token. See [diskcopilot-cli](https://github.com/diskcopilot/diskcopilot-cli#privacy--security) for details.

## License

MIT
