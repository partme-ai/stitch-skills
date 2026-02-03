<div align="center">

# Stitch Skills

**Agent Skills Collection for Stitch UI Generation**

![Version](https://img.shields.io/badge/Version-1.0.0-blue)
![License](https://img.shields.io/badge/License-Apache%202.0-green)
![Skills](https://img.shields.io/badge/Skills-13-orange)
![Plugins](https://img.shields.io/badge/Plugins-3-brightgreen)

</div>

## 📖 Introduction

**Stitch Skills** is a collection of Agent Skills designed to empower AI agents (like Claude, Trae) to autonomously design and generate UI screens using the Stitch MCP. It follows the [Agent Skills Specification](https://agentskills.io/) and provides a "Self-Looping" design workflow.

## 🔗 Official Resources

Key documentation from the official Stitch team:

*   **[Overview](https://stitch.withgoogle.com/docs/learn/overview/)**: Introduction to Stitch capabilities.
*   **[Prompting Guide](https://stitch.withgoogle.com/docs/learn/prompting/)**: Best practices for writing effective design prompts.
*   **[Device Types](https://stitch.withgoogle.com/docs/learn/device-types/)**: Understanding Mobile, Desktop, and Web layouts.
*   **[Design Modes](https://stitch.withgoogle.com/docs/learn/design-modes/)**: Standard (Flash) vs Experimental (Pro) modes.
*   **[Variants](https://stitch.withgoogle.com/docs/learn/variants/)**: Generating and managing design variations.
*   **[Controls](https://stitch.withgoogle.com/docs/learn/controls/)**: Using interactive controls to refine designs.
*   **[MCP Guide](https://stitch.withgoogle.com/docs/mcp/guide/)**: Technical guide for Model Context Protocol integration.

## 🔌 MCP Setup (Required for real execution)

This repository contains **skills and tool schemas**, but it does **not** ship the Stitch MCP Server itself.

To actually create projects and generate screens, you must:

*   Configure Stitch MCP Server using the official guide: https://stitch.withgoogle.com/docs/mcp/guide/
*   Ensure your client exposes the Stitch MCP tools (tool names in this repo's `docs/*.json`):
    *   `create_project`
    *   `list_projects`
    *   `get_project`
    *   `generate_screen_from_text`
    *   `list_screens`
    *   `get_screen`

In some clients, MCP tools are **namespaced** and may appear as:

*   `mcp__<serverName>__create_project`
*   `mcp__<serverName>__generate_screen_from_text`

`<serverName>` must match the name you configured in `mcpServers`.

## 🏗️ Architecture

The skills are organized into logical layers to enable autonomous "Design -> Execute" loops.

- **`stitch-ui-*`**: **The Brain**. Skills that handle design logic, prompt engineering, and orchestration. No external API costs.
- **`stitch-mcp-*`**: **The Hands**. Wrappers around the Stitch MCP (Model Context Protocol). These execute the actual API calls.

```text
stitch-skills/
├── skills/
│   ├── stitch-ui-designer/          # [Orchestrator] Master skill
│   ├── stitch-ui-design-spec-generator/ # [Logic] Style & Spec logic
│   ├── stitch-ui-prompt-architect/      # [Logic] Prompt Engineering
│   ├── stitch-mcp-project-create/   # [Execution] Create Project
│   ├── stitch-mcp-screen-generate/  # [Execution] Generate UI
│   ├── stitch-skill-creator/        # [Meta] Create new skills
│   └── ...
├── docs/                            # API Specifications
├── media/                           # Assets
├── LICENSE                          # Apache 2.0
└── README.md                        # Documentation
```

## 📦 Available Skills

### Orchestrator (The Entry Point)
*   **`stitch-ui-designer`**: The Master Skill. Invokes it to handle end-to-end design tasks (e.g., "Design a login page"). It automatically coordinates logic and execution skills.

### Logic & Design Skills (The Brain)
*   **`stitch-ui-design-spec-generator`**: Analyzes vague user requests to output structured design specifications (Theme, Device, Style).
*   **`stitch-ui-prompt-architect`**: Converts specifications into detailed, high-quality Stitch Prompts following best practices.
*   **`stitch-ui-design-variants`**: Generates design variations (A/B testing ideas) for a given screen concept.

### Execution Skills (The Hands - MCP)
*   **`stitch-mcp-project-create`**: Create new Stitch projects.
*   **`stitch-mcp-project-list`**: List existing projects.
*   **`stitch-mcp-project-get`**: Get project details.
*   **`stitch-mcp-screen-generate`**: **Core** Text-to-UI generation.
*   **`stitch-mcp-screen-list`**: List generated screens.
*   **`stitch-mcp-screen-get`**: Export screen code/assets.
*   **`stitch-mcp-screen-refine`**: Refine or edit an existing screen.

### Atomic Tools
*   **`stitch-skill-creator`**: An atomic tool for generating new **Scenario Skills** (e.g., `stitch-ui-music-designer`) from a "Golden Template". Enforces SOP compliance.
*   **`stitch-ui-design-spec-uview`**: uView 2.0 (uni-app / Vue2) design spec tool.
*   **`stitch-ui-design-spec-uviewpro`**: uView Pro (uni-app / Vue3) design spec tool.
*   **`stitch-ui-design-spec-layui`**: Layui-Vue (Vue 3.0) design spec tool.
*   **`stitch-ui-design-spec-bootstrap`**: Bootstrap-Vue (Bootstrap 5) design spec tool.
*   **`stitch-ui-design-spec-element-plus`**: Element Plus (Vue 3) design spec tool.
*   **`stitch-ui-design-spec-vant`**: Vant 4 (Vue 3 / Mobile) design spec tool.

### Knowledge Skills
*   **`stitch-ued-guide`**: Design guidelines, visual vocabulary, and prompt strategies used by other skills.

## 🚀 Quick Start

### 1) Install (Claude Code)

Register this repository as a marketplace:

```bash
/plugin marketplace add https://github.com/partme-ai/stitch-skills.git
```

### 1b) Install (Trae)

Trae loads skills from either:

- Project-local: `.trae/skills/` in your current workspace
- Global: `~/.trae/skills/` (or `~/.trae-cn/skills/`)

Copy/link `stitch-skills/skills/*` into one of these locations.

### 2) Configure MCP (Required for real execution)

Make sure your client is configured with the Stitch MCP server and exposes MCP tools like:

- `create_project`
- `generate_screen_from_text`
- `list_projects`
- `list_screens`
- `get_screen`

### 3) Use

Example:

> "Use stitch to implement 登录_PRD.md UI requirements (Login + Register)."
> "Use Stitch and Layui style to design a dashboard for an admin system."
> "Use Stitch and Bootstrap style to design a landing page."
> "Use Stitch and Element Plus style to design a CRM dashboard."
> "Use Stitch and uView Pro style to design a mobile app home screen."

Expected tool chain:

1. `create_project`
2. `generate_screen_from_text` (Login)
3. `generate_screen_from_text` (Register)
4. `list_screens`
5. `get_screen`

## 🔒 Safety & Triggers

All execution skills (`stitch-mcp-*`) and the master orchestrator (`stitch-ui-designer`) are protected by a **Critical Prerequisite**: they will only trigger when the user **explicitly mentions "Stitch"**. This prevents accidental API usage during normal conversation.

## 📄 License

Apache 2.0
