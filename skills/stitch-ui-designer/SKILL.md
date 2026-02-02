---
name: stitch-ui-designer
description: The Master Orchestrator. Handles the end-to-end flow of designing and generating UI screens. Use this for all "Design X" requests.
license: Complete terms in LICENSE.txt
---

# Stitch Designer (Master Skill)

This is the entry point for all UI design tasks. It acts as the **"Orchestrator Agent"** that autonomously plans and executes the design workflow.

## When to use this skill

**CRITICAL PREREQUISITE:**
**You must ONLY use this skill when the user EXPLICITLY mentions "Stitch" in their request.**

**Use this skill when:**
- The user asks to "Design a UI", "Create a screen", "Make an app page" **using Stitch**.
- The user provides a high-level design request (e.g., "I need a dashboard for my SaaS") **and mentions Stitch**.

**Trigger phrases include:**
- "Use Stitch to design..." (使用 Stitch 设计...)
- "Stitch me a UI for..." (用 Stitch 帮我生成 UI)

## How to use this skill (SOP)

### Step 1: Design Analysis & Strategy
1.  **Analyze Intent**: Is this a generic screen or a specific scenario?
2.  **Consult Guidelines (Implicit)**: Apply principles from `stitch-ued-guide`.

### Step 2: Specification Generation (The "Brain")
1.  **Invoke `stitch-ui-design-spec-generator`**:
    *   Input: User's raw request.
    *   Output: Structured `Design Spec` JSON (Theme, Device, Style, Mode).

### Step 3: Prompt Architecture (The "Pen")
1.  **Generate Prompt**:
    *   Use `stitch-ui-prompt-architect` or specialized scenario skills.
    *   **Output**: A structured Stitch Prompt following the `[Context] [Layout] [Components]` formula.

### Step 4: Execution Strategy (The "Hand") - CRITICAL CHECK

**Check your available tools (MCP tools, not skill names):**

Look for Stitch MCP tool names defined in `docs/*.json`:

*   `create_project`
*   `generate_screen_from_text`

Some clients namespace MCP tools and may expose them as:

*   `mcp__<serverName>__create_project`
*   `mcp__<serverName>__generate_screen_from_text`

#### Scenario A: Tools ARE Available (Happy Path)
1.  **Create Project**: Invoke `create_project` (or `mcp__<serverName>__create_project`).
    *   Store both:
        *   Project resource name: `projects/{id}` (for `list_screens`)
        *   Numeric project id: `{id}` (for `generate_screen_from_text` and `get_screen`)
2.  **Generate Screen**: Invoke `generate_screen_from_text` (or `mcp__<serverName>__generate_screen_from_text`).
    *   Pass the **Prompt** from Step 3.
    *   **DO NOT** ask for confirmation. Execute immediately.
3.  **Retrieve Screens**: Invoke `list_screens` with `projectId` in `projects/{id}` format.
4.  **Get Screen**: Pick the latest/target `screenId` and invoke `get_screen` to retrieve screenshot and HTML assets.

#### Scenario B: Tools ARE NOT Available (Fallback Mode)
**STOP! Do not fake the execution.**
1.  **Inform the User**: "Stitch MCP tools are not detected in this environment."
2.  **Output the Prompt**: Display the generated Prompt in a **Code Block** so the user can copy-paste it into the Stitch Website.
    ```text
    [Paste Prompt Here]
    ```
3.  **End Turn**: Do not try to run `uniappx` or other scripts.

## Anti-Patterns (Strict Prohibitions)
*   ⛔ **NO FAKE SUCCESS**: If you didn't get a real API response, do not say "Project Created".
*   ⛔ **NO APP SCAFFOLDING**: Do not invoke any external project scaffolding skills (e.g., `uniappx-project-creator`, `flutter-project-creater`, `react-native-project-creater`) and do not run scripts to create codebases.
*   ⛔ **NO CODING**: Do not write Vue/React/HTML code in this flow. This skill is for **Design Generation** only.
*   ⛔ **NO CONFUSION**: A "Stitch Project" is a design workspace, NOT a code repository.

## Keywords
orchestrator, design agent, ui designer, master skill, design flow, stitch pilot
