# AGENTS.md

This document provides guidance for AI coding agents (Claude Code, Cursor, Copilot, etc.) working within this repository.

## Repository Overview

A collection of Agent Skills for Stitch UI Generation. Skills are packaged instructions and scripts that extend Claude's capabilities.

## Skill Structure

```
skills/
  {skill-name}/           # kebab-case directory name
    SKILL.md              # Required: skill definition
    examples/             # Required: usage examples
      usage.md
    LICENSE.txt           # Required: license file
```

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
