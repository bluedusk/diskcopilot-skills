# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A Claude Code plugin that teaches AI agents how to use `diskcopilot-cli` for macOS disk scanning, analysis, and cleanup. There is no compiled code -- the entire plugin is markdown instruction files and JSON metadata.

Also works with other agents (Cursor, Copilot, Codex, Windsurf, Gemini CLI) by copying SKILL.md into their config files -- see README.md for the config file mapping.

## Repository Structure

- `.claude-plugin/plugin.json` -- plugin manifest (name, version, metadata)
- `.claude-plugin/marketplace.json` -- marketplace listing for `claude plugin marketplace add`
- `skills/diskcopilot/SKILL.md` -- the core skill: complete instructions, SQLite schema, SQL examples, CLI reference. This is the "brain" of the plugin.
- `skills/diskcopilot/references/macos-junk.md` -- reference data for SKILL.md: known junk categories, cleanup SQL queries, and safe-delete commands
- `commands/*.md` -- three slash commands (`scan`, `cleanup`, `report`) that orchestrate the skill for specific workflows
- `evals/evals.json` -- evaluation prompts to test skill effectiveness (3 scenarios)
- `disk-analysis-workspace/` -- gitignored eval artifacts (before/after comparisons)

## Architecture

The plugin follows an instruction-driven pattern:

1. **SKILL.md** contains all knowledge: CLI installation, SQLite schema docs, example SQL queries, predefined commands, safety rules, and example flows. The `references/` subdirectory holds supplementary data (e.g., macOS junk categories) that the skill references.
2. **Commands** are thin orchestrators that reference the skill and add step-by-step workflows. They delegate via "Use the diskcopilot skill for instructions" -- they don't duplicate skill content.
3. The plugin auto-installs `diskcopilot-cli` binary to `~/.local/bin` on first use (no sudo)

The skill defines three response modes that map to the commands:
- **Report** (`/diskcopilot:report`) -- full Disk Health Report with categorized cleanup opportunities and health score
- **Quick query** -- answer a specific question with a SQL query, no full report
- **Cleanup** (`/diskcopilot:cleanup`) -- report + interactive deletion with `diskcopilot-cli delete <path> --trash`

`/diskcopilot:scan` is a utility command that just ensures a cache exists.

## Running Evaluations

Evals are defined in `evals/evals.json` (3 scenarios). Artifacts go to `disk-analysis-workspace/` (gitignored). There is no build step, linter, or test runner -- this is a documentation-only project.

## Key Conventions

- **Sizes**: always bytes in SQL/JSON, displayed with decimal units (1 GB = 1,000,000,000 bytes, matching macOS/Finder)
- **Deletion**: always `--trash` (recoverable), never `--permanent` unless user explicitly requests it
- **Scanning**: always scan `/` (whole drive) with `--force` to skip the system path warning. One scan covers everything -- no need to re-scan subdirectories.
- **Cache check**: always run `diskcopilot-cli query info /` before scanning. If a cache exists, ask the user before rescanning.

## Extending the Plugin

- **New command**: add a `.md` file to `commands/` with YAML frontmatter (`description` field) and step-by-step instructions that reference the skill
- **New capability**: update `skills/diskcopilot/SKILL.md` with SQL examples, CLI flags, or safety guidelines. Add reference data to `skills/diskcopilot/references/`.
- **New eval**: add an entry to `evals/evals.json` with `id`, `prompt`, and `expected_output`
