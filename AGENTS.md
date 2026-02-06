# AGENTS.md

This document provides guidance for AI coding agents (Claude Code, Cursor, Copilot, etc.) working within this repository.

## Recommended Agent

For Stitch-based UI generation (text-to-UI, design specs, MCP workflows), use the **stitch-ui-designer** agent. Agent file: [agents/stitch-ui-designer.md](agents/stitch-ui-designer.md) (same format as [fullstack-engineer](https://github.com/anthropics/claude-usage/blob/main/agents/fullstack-engineer.md)).

## Repository Overview

A collection of Agent Skills for Stitch UI Generation. Skills are packaged instructions and scripts that extend Claude's capabilities. This repo **subsumes and strengthens** [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills): every official skill (design-md, enhance-prompt, stitch-loop, react-components, remotion, shadcn-ui) has a local equivalent that is better or equal and integrated with stitch-mcp-* and framework design specs. See [docs/related-upstream.md](docs/related-upstream.md). 本仓库技能参与**「需求→部署」全链路**（PRD→原型与设计、设计规范、UI 说明、界面与交互）。本库阶段→技能一览见 [docs/pipeline-stage-to-stitch-skills.md](docs/pipeline-stage-to-stitch-skills.md)，完整全链路映射见 [full-stack-skills/docs/pipeline-stage-to-skills.md](../full-stack-skills/docs/pipeline-stage-to-skills.md)，技能生态见 [full-stack-skills/docs/skills-ecosystem.md](../full-stack-skills/docs/skills-ecosystem.md)（同 workspace 内）。

## Skill Structure

Each skill directory follows the Agent Skills standard (see [spec/agent-skills-spec.md](spec/agent-skills-spec.md)):

```
skills/{skill-name}/      # kebab-case directory name
├── SKILL.md              # Required: skill definition (Mission Control)
├── examples/             # Required: usage examples (gold-standard reference)
│   └── usage.md
├── references/          # Optional: contracts, style guides, checklists
├── scripts/              # Optional: validation, fetch, or codegen scripts
└── LICENSE.txt           # Required: license file
```

- **SKILL.md**: Frontmatter (`name`, `description`); optional `allowed-tools` to restrict tools when this skill is active.
- **examples/**: Syntactically valid references for few-shot use.
- **references/** / **scripts/**: Load on demand to keep context small.

## SKILL.md Format

```markdown
---
name: {skill-name}
description: {One sentence describing when to use this skill.}
---

# {Skill Title}

{Brief description of what the skill does.}

## Tools

{List of MCP tools wrapped by this skill, if any}

## Usage Patterns

{How to use this skill effectively}
```

## Context Efficiency Best Practices

Skills are loaded on demand. To reduce context usage:
- **Keep SKILL.md under 500 lines**.
- **Write specific descriptions** to help the agent decide when to activate.
- **Progressive disclosure**: Reference supporting files, read only when needed.

## Installing for End Users

**Claude Code:**
```bash
/plugin marketplace add https://github.com/partme-ai/stitch-skills.git
/plugin install stitch-ui@stitch-skills
/plugin install stitch-mcp@stitch-skills
```

## MCP Prerequisite (Why tools may not run)

This repository provides **skills** and **tool schemas** only. If you don't have the Stitch MCP Server configured, the agent will not be able to call tools like `create_project` or `generate_screen_from_text`.

Follow the official MCP setup guide:
https://stitch.withgoogle.com/docs/mcp/guide/
