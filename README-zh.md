# claude-custom-skills

[English](README.md)

> 专为 [Claude Code](https://claude.ai/code) 设计的自定义斜线命令与自动化技能集合——涵盖生产力工具、数据导出、内容工作流等多种场景。

[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Claude Skills](https://img.shields.io/badge/claude%20skills-3-purple)](#命令与技能)

---

## 目录

- [概述](#概述)
- [前提条件](#前提条件)
- [命令与技能](#命令与技能)
  - [数据与生产力](#数据与生产力)
- [安装](#安装)
- [使用说明](#使用说明)
- [贡献指南](#贡献指南)
- [许可证](#许可证)

---

## 概述

本仓库收录了可直接投入使用的 **Claude Code 技能**与**斜线命令**，用于为 Claude Code 扩展自定义自动化工作流。

**技能**（`.skill` 文件）是用于扩展 Claude Code 功能的自定义能力，在任意 Claude Code 会话中通过 `/技能名称` 调用。

**命令**（`.claude/commands/`）是斜线命令定义及相关支持脚本。如需在某个项目中使用全部命令，将 `.claude/` 文件夹复制到该项目根目录即可；如需在所有项目中全局使用，则复制到 `~/.claude/`。

---

## 前提条件

- 已安装并完成身份验证的 [Claude Code](https://claude.ai/code)
- Python 3.8+（适用于需要运行 Python 脚本的命令）

---

## 命令与技能

### 数据与生产力

| 名称 | 类型 | 触发命令 | 描述 |
|---|---|---|---|
| [`export-twitter-bookmarks`](./twitter-bookmarks-exporter/) | 技能 | `/export-twitter-bookmarks` | 将所有 X/Twitter 书签导出为独立的 Markdown 文件并附加元数据；支持多页 JSON、普通推文/长文推文/X 文章的完整文本提取、t.co 短链还原、引用推文、媒体链接以及互动数据统计 |
| [`perplexity-downloader`](./perplexity-downloader/) | 技能 | `/perplexity-downloader` | 将 Perplexity.ai 对话线程下载并导出为独立的 Markdown 文件；支持单条线程、批量 URL 列表或完整历史记录导出，并自动生成索引文件 |
| [`readme-i18n`](./readme-i18n/) | 技能 | `/readme-i18n` | 将 `README.md` 同步翻译为简体中文版（`README-zh.md`），以英文为主要内容来源；自动在两个文件顶部添加互跳链接，并在翻译前校正语法及拼写错误 |

---

## 安装

### 技能

技能可直接在 Claude Code 中导入：

1. 在 Claude Code 中，进入 **Settings（设置）** → **Skills（技能）**
2. 点击 **Import（导入）** 或 **+** 添加自定义技能
3. 选择本仓库中的 `.skill` 文件
4. 技能即可在当前 Claude Code 会话中使用

### 命令（项目级）

```bash
git clone https://github.com/negtivSpaz/claude-custom-skills.git
cp -r claude-custom-skills/.claude /your/project/
```

### 命令（全局——在所有项目中可用）

```bash
git clone https://github.com/negtivSpaz/claude-custom-skills.git
cp -r claude-custom-skills/.claude ~/.claude/
```

### 单个命令

将 `.claude/commands/` 中所需的特定文件复制到项目的 `.claude/commands/` 目录下即可。

---

## 使用说明

### 使用技能

在任意 Claude Code 会话中，输入技能命令：

```
/perplexity-downloader https://www.perplexity.ai/search/your-query
```

也可以通过自然语言描述技能意图来触发。

### 使用命令

在任意 Claude Code 会话中，输入斜线命令：

```
/export-twitter-bookmarks
```

Claude 会引导你完成所有缺失的前提步骤，并端到端地执行整个工作流。

每个技能的详细文档位于其对应文件夹中（例如 `perplexity-downloader/README.md`）；每个命令的完整输入/输出说明记录在 `.claude/commands/<name>.md` 文件中；相关支持脚本与之并列存放（例如 `twitter-bookmarks-exporter/scripts/`）。

---

## 贡献指南

### 添加技能

1. Fork 本仓库并创建功能分支：`git checkout -b feat/my-skill`
2. 新建目录：`mkdir my-skill`
3. 创建 `my-skill.skill` 文件（包含 `SKILL.md` 的 ZIP 压缩包）
   - `SKILL.md` 应包含元数据（名称、描述）及详细文档
4. 在目录中添加 `README.md`，说明安装步骤、使用方法及示例
5. 在 Claude Code 中导入 `.skill` 文件进行本地测试
6. 向 `main` 分支发起 Pull Request，附上功能描述和调用示例

### 添加命令

1. Fork 本仓库并创建功能分支：`git checkout -b feat/my-command`
2. 在 `.claude/commands/<command-name>.md` 下添加命令文件
   - 文件名即为斜线命令触发词（例如 `my-tool.md` → `/my-tool`）
3. 将相关支持脚本放置于同名文件夹下（例如 `my-tool/scripts/`）
4. 在 Claude Code 会话中进行本地测试
5. 向 `main` 分支发起 Pull Request，附上功能描述和调用示例

---

## 许可证

本项目采用 [MIT 许可证](LICENSE)。
