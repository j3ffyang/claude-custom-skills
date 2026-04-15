# claude-custom-skills

> A curated collection of custom slash commands and automation skills for [Claude Code](https://claude.ai/code) — covering productivity, data export, content workflows, and more.

[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Claude Commands](https://img.shields.io/badge/claude%20commands-1-purple)](#commands)

---

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Commands](#commands)
  - [Data & Productivity](#data--productivity)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

This repository hosts production-ready **Claude Code slash commands** (`.claude/commands/`) and their supporting scripts. Each command extends Claude Code with a specific automation workflow — invoked simply by typing `/command-name` in any Claude Code session.

To use all commands in a project, copy the `.claude/` folder into your project root. To use them globally across all projects, copy to `~/.claude/`.

---

## Prerequisites

- [Claude Code](https://claude.ai/code) installed and authenticated
- Python 3.8+ (for commands that run Python scripts)

---

## Commands

### Data & Productivity

| Command | Trigger | Version | Description |
|---|---|---|---|
| [`export-twitter-bookmarks`](./.claude/commands/export-twitter-bookmarks.md) | `/export-twitter-bookmarks` | 1.2.0 | Export X/Twitter bookmarks into individual Markdown files; handles multi-page JSON, full text for regular/note/article tweets, t.co URL expansion, quoted tweets, media links, and engagement stats |

---

## Installation

### All commands (project-level)

```bash
git clone https://github.com/negtivSpaz/claude-custom-skills.git
cp -r claude-custom-skills/.claude /your/project/
```

### All commands (global — available in every project)

```bash
git clone https://github.com/negtivSpaz/claude-custom-skills.git
cp -r claude-custom-skills/.claude ~/.claude/
```

### Single command

Copy the specific file from `.claude/commands/` into your project's `.claude/commands/` folder.

---

## Usage

Inside any Claude Code session, type the slash command:

```
/export-twitter-bookmarks
```

Claude will guide you through any missing prerequisites and run the workflow end-to-end.

Each command's full input/output contract is documented in its `.claude/commands/<name>.md` file. Supporting scripts live alongside under the skill's own folder (e.g., `twitter-bookmarks-exporter/scripts/`).

---

## Contributing

1. Fork this repository and create a feature branch: `git checkout -b feat/my-command`
2. Add your command file under `.claude/commands/<command-name>.md`
   - The filename becomes the slash command trigger (e.g., `my-tool.md` → `/my-tool`)
3. Add any supporting scripts under a matching folder (e.g., `my-tool/scripts/`)
4. Test locally inside a Claude Code session
5. Open a pull request against `main` with a description and example invocation

---

## License

This project is licensed under the [MIT License](LICENSE).
