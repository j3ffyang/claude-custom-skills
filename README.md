# claude-custom-skills

> A curated collection of custom slash commands and automation skills for [Claude Code](https://claude.ai/code) — covering productivity, data export, content workflows, and more.

[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Claude Skills](https://img.shields.io/badge/claude%20skills-2-purple)](#commands--skills)

---

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Commands & Skills](#commands--skills)
  - [Data & Productivity](#data--productivity)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

This repository hosts production-ready **Claude Code skills** and **slash commands** for extending Claude Code with custom automation workflows.

**Skills** (`.skill` files) are custom capabilities that extend Claude Code functionality. Invoke them with `/skill-name` in any Claude Code session.

**Commands** (`.claude/commands/`) are slash command definitions and supporting scripts. To use all commands in a project, copy the `.claude/` folder into your project root. To use them globally across all projects, copy to `~/.claude/`.

---

## Prerequisites

- [Claude Code](https://claude.ai/code) installed and authenticated
- Python 3.8+ (for commands that run Python scripts)

---

## Commands & Skills

### Data & Productivity

| Name | Type | Trigger | Description |
|---|---|---|---|
| [`export-twitter-bookmarks`](./.claude/commands/export-twitter-bookmarks.md) | Command | `/export-twitter-bookmarks` | Export X/Twitter bookmarks into individual Markdown files; handles multi-page JSON, full text for regular/note/article tweets, t.co URL expansion, quoted tweets, media links, and engagement stats |
| [`perplexity-downloader`](./perplexity-downloader/) | Skill | `/perplexity-downloader` | Download and export Perplexity.ai conversation threads as individual Markdown files; supports single thread, bulk URL lists, or full history export with automatic index generation |

---

## Installation

### Skills

Skills are imported directly in Claude Code:

1. In Claude Code, go to **Settings** → **Skills**
2. Click **Import** or **+** to add a custom skill
3. Select the `.skill` file from this repository
4. The skill is now available in your Claude Code session

### Commands (project-level)

```bash
git clone https://github.com/negtivSpaz/claude-custom-skills.git
cp -r claude-custom-skills/.claude /your/project/
```

### Commands (global — available in every project)

```bash
git clone https://github.com/negtivSpaz/claude-custom-skills.git
cp -r claude-custom-skills/.claude ~/.claude/
```

### Single command

Copy the specific file from `.claude/commands/` into your project's `.claude/commands/` folder.

---

## Usage

### Using Skills

Inside any Claude Code session, type the skill command:

```
/perplexity-downloader https://www.perplexity.ai/search/your-query
```

Or trigger naturally by referencing the skill's intent.

### Using Commands

Inside any Claude Code session, type the slash command:

```
/export-twitter-bookmarks
```

Claude will guide you through any missing prerequisites and run the workflow end-to-end.

Each skill's documentation is in its respective folder (e.g., `perplexity-downloader/README.md`). Each command's full input/output contract is documented in its `.claude/commands/<name>.md` file. Supporting scripts live alongside (e.g., `twitter-bookmarks-exporter/scripts/`).

---

## Contributing

### Adding a Skill

1. Fork this repository and create a feature branch: `git checkout -b feat/my-skill`
2. Create a new directory: `mkdir my-skill`
3. Create a `my-skill.skill` file (ZIP archive containing `SKILL.md`)
   - `SKILL.md` should include metadata (name, description) and detailed documentation
4. Add a `README.md` in the directory documenting installation, usage, and examples
5. Test locally by importing the `.skill` file in Claude Code
6. Open a pull request against `main` with a description and example invocation

### Adding a Command

1. Fork this repository and create a feature branch: `git checkout -b feat/my-command`
2. Add your command file under `.claude/commands/<command-name>.md`
   - The filename becomes the slash command trigger (e.g., `my-tool.md` → `/my-tool`)
3. Add any supporting scripts under a matching folder (e.g., `my-tool/scripts/`)
4. Test locally inside a Claude Code session
5. Open a pull request against `main` with a description and example invocation

---

## License

This project is licensed under the [MIT License](LICENSE).
