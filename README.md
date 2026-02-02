<div align="center">

# Stitch Skills

**Agent Skills Collection for Stitch UI Generation**

![Version](https://img.shields.io/badge/Version-1.0.0-blue)
![License](https://img.shields.io/badge/License-Apache%202.0-green)
![Skills](https://img.shields.io/badge/Skills-13-orange)

</div>

## 📖 Introduction

**Stitch Skills** is a collection of Agent Skills designed to empower AI agents (like Claude, Trae) to autonomously design and generate UI screens using the Stitch MCP. It follows the [Agent Skills Specification](https://agentskills.io/) and provides a "Self-Looping" design workflow.

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

### Meta Skills (Tooling)
*   **`stitch-skill-creator`**: A utility to generate new **Scenario Skills** (e.g., `stitch-ui-music-designer`) from a "Golden Template". Enforces SOP compliance.

### Knowledge Skills
*   **`stitch-ued-guide`**: Design guidelines, visual vocabulary, and prompt strategies used by other skills.

## 🚀 Quick Start

1.  **Install**: Add this repository as a skill source to your Agent.
2.  **Use**: Simply ask the Agent:
    > "Use Stitch to design a cyberpunk login page."
3.  **Watch**: The Agent will autonomously:
    *   **Analyze** style (Cyberpunk -> Dark/Neon) using `stitch-ui-design-spec-generator`.
    *   **Create** a project using `stitch-mcp-project-create`.
    *   **Architect** a detailed prompt using `stitch-ui-prompt-architect`.
    *   **Generate** the screen using `stitch-mcp-screen-generate`.
    *   **Return** the result.

## 🔒 Safety & Triggers

All execution skills (`stitch-mcp-*`) and the master orchestrator (`stitch-ui-designer`) are protected by a **Critical Prerequisite**: they will only trigger when the user **explicitly mentions "Stitch"**. This prevents accidental API usage during normal conversation.

## 📄 License

Apache 2.0
