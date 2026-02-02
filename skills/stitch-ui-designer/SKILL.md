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
*   ✅ "Use Stitch to design a login page"
*   ✅ "Help me design a dashboard with Stitch"
*   ❌ "Design a login page" (Ignore, unless previous context established Stitch)

**Use this skill when:**
- The user asks to "Design a UI", "Create a screen", "Make an app page" **using Stitch**.
- The user provides a high-level design request (e.g., "I need a dashboard for my SaaS") **and mentions Stitch**.
- You want to execute the full "Think -> Plan -> Execute" design loop.
- You are unsure which specific atomic skill to call first.

**Trigger phrases include:**
- "Use Stitch to design..." (使用 Stitch 设计...)
- "Stitch me a UI for..." (用 Stitch 帮我生成 UI)
- "Create a Stitch project" (创建一个 Stitch 项目)
- "Stitch generate screen" (Stitch 生成页面)

## How to use this skill (SOP)

When the user asks to design a UI, follow this **Self-Looping Process** immediately. **Do not stop to ask for confirmation.**

### Step 1: Design Analysis & Strategy
1.  **Analyze Intent**: Is this a generic screen or a specific scenario?
    *   *Check for Specialized Skills*: Search for available `stitch-ui-*-designer` skills that match the request (e.g., Music, Login).
    *   *If Match Found* -> Use the specialized skill.
    *   *If No Match* -> Proceed to Step 2 (General Flow).
2.  **Consult Guidelines (Implicit)**: Apply principles from `stitch-ued-guide` (e.g., mobile-first, visual hierarchy).

### Step 2: Specification Generation (The "Brain")
*If a specific Scenario Skill was selected in Step 1, skip to Step 3.*

1.  **Invoke `stitch-ui-design-spec-generator`**:
    *   Input: User's raw request.
    *   Output: Structured `Design Spec` JSON (Theme, Device, Style, Mode).
    *   *Reasoning*: This ensures we have concrete parameters (e.g., "Dark Mode", "Mobile") before writing the prompt.

### Step 3: Prompt Architecture (The "Pen")
1.  **If Scenario Skill Selected**:
    *   **Invoke Scenario Skill** (e.g., `stitch-ui-music-designer`).
    *   Input: User request + inferred style.
    *   Output: A highly specialized, battle-tested Stitch Prompt.
2.  **If General Flow**:
    *   **Invoke `stitch-ui-prompt-architect`**.
    *   Input: User request + `Design Spec` from Step 2.
    *   Output: A structured Stitch Prompt following the `[Context] [Layout] [Components]` formula.

### Step 4: Project Context (The "Canvas")
1.  **Check Context**: Do we have an active `projectId` in conversation history?
2.  **If No**: Invoke `stitch-mcp-project-create`.
    *   Title: Derived from user request (e.g., "Cyberpunk Auth App").
    *   *Action*: Store the returned `name` (Project ID).
3.  **If Yes**: Use existing ID.

### Step 5: Execution (The "Hand")
1.  **Invoke `stitch-mcp-screen-generate`**:
    *   `projectId`: From Step 4.
    *   `prompt`: The **Final Prompt** from Step 3.
    *   `deviceType`: From Design Spec or Scenario Default.
    *   `modelId`: `GEMINI_3_PRO` (Always use Pro for design tasks).

### Step 6: Presentation
1.  **Show Result**: Present the generated screen screenshot.
2.  **Self-Correction (Optional)**: If the result looks wrong (e.g., text overlap), internally trigger `stitch-mcp-screen-refine` before showing to user (Advanced).

## Best Practices

1.  **Bias for Action**: Don't ask "Should I create a project?". Just create it. Don't ask "What style?". Infer it or use `stitch-ui-design-spec-generator`.
2.  **Self-Correction**: If a tool call fails (e.g., invalid ID), try to list projects to find the correct ID, or create a new one.
3.  **Show, Don't Just Tell**: Always display the visual result (Screenshot URL).

## Keywords

**English keywords:**
orchestrator, design agent, ui designer, master skill, design flow, automated design, stitch pilot

**Chinese keywords (中文关键词):**
设计编排, UI代理, 设计助手, 全流程设计, 自动设计, 界面生成向导
