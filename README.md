# diskcopilot

[![Version](https://img.shields.io/badge/version-0.3.0-blue)](https://github.com/bluedusk/diskcopilot-skills/releases)

AI agent plugin for disk scanning, analysis, and cleanup. Requires macOS.

Teaches AI agents how to use [diskcopilot-cli](https://github.com/bluedusk/diskcopilot-cli) — a fast disk scanner (~12s for a home directory) that caches filesystem metadata in SQLite, letting the agent write SQL to answer any disk space question.

Ask your agent things like:
- "What's taking up space on my Mac?"
- "How big are my node_modules?"
- "Help me free up 10GB"

## Install

### Claude Code

```bash
claude plugin marketplace add bluedusk/diskcopilot-skills
claude plugin install diskcopilot
```

The plugin will automatically install the `diskcopilot-cli` binary on first use.

### Other agents (Cursor, Copilot, Codex, Windsurf, etc.)

Copy the skill instructions from [skills/diskcopilot/SKILL.md](skills/diskcopilot/SKILL.md) into your agent's configuration file:

| Agent | Config file |
|-------|-------------|
| Cursor | `.cursorrules` or `.cursor/rules/*.mdc` |
| GitHub Copilot | `.github/copilot-instructions.md` |
| OpenAI Codex | `AGENTS.md` |
| Windsurf | `.windsurfrules` |
| Google Gemini CLI | `GEMINI.md` |

The skill includes auto-install instructions for the CLI binary — no manual setup needed.

## Commands

| Command | What it does |
|---------|-------------|
| `/diskcopilot:scan` | Scan a directory (or cwd) and cache metadata |
| `/diskcopilot:cleanup` | Analyze + open browser dashboard to select and trash items |
| `/diskcopilot:report` | Analyze + show report in conversation |

## Privacy

`diskcopilot-cli` only reads filesystem metadata (names, sizes, timestamps). It has no network dependencies and never sends data anywhere. The interactive cleanup UI runs on localhost with a per-session auth token. See [diskcopilot-cli](https://github.com/bluedusk/diskcopilot-cli#privacy--security) for details.

## License

MIT
