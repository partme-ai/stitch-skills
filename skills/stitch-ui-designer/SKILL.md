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

## Workflow (Flow-first, copy-pastable)

This skill must follow this workflow end-to-end. Do not skip steps.

### 0) Preflight (Tool Availability)

1. Detect whether Stitch MCP tools are available.
2. If tools are available, follow the **Execution workflow**.
3. If tools are not available, follow the **Prompt-only workflow**.

### 1) Intent Classification

Determine the task type:

- **New screen**: design + generate a new UI screen.
- **Refine / Beautify**: modify an existing screen while preserving layout and information architecture.

### 2) Design Spec Workflow (Brain)

Invoke `stitch-ui-design-spec-generator` with the user request.

Expected result:

- A structured `Design Spec` JSON (Theme, Device, Style, Mode).

### 3) Contract Workflow (Hard Constraints)

If the request includes a named design system / style, fetch constraints from the matching design contract tool and inject them into the final prompt.

Supported mapping (Match Priority: Specific > General):

- `uview-pro`, `uviewpro`, `uview pro` -> use `stitch-ui-design-spec-uviewpro` (Match this FIRST)
- `uview`, `uview2`, `uview2.0`, `u-view` -> use `stitch-ui-design-spec-uview`
- `layui`, `layui-vue`, `layui vue` -> use `stitch-ui-design-spec-layui`
- `bootstrap`, `bootstrap-vue`, `bs-vue` -> use `stitch-ui-design-spec-bootstrap`
- `element`, `element-plus`, `el-plus`, `element-ui` -> use `stitch-ui-design-spec-element-plus`
- `vant`, `vant4`, `vant-ui` -> use `stitch-ui-design-spec-vant`

Decision rules:

- If the user asks for refine/beautify, or explicitly asks for selector / JSON / `contracts.include` / `states.include`:
  - Use `stitch-ui-design-spec-uview` or `stitch-ui-design-spec-layui` in **selector mode**.
  - Treat the returned selection JSON as internal and use the assembled prompt as the execution prompt.
- Otherwise:
  - Use `stitch-ui-design-spec-uview` or `stitch-ui-design-spec-layui` in **prefix mode**.
  - Prepend the returned prefix to `[Context]`.

### 4) Prompt Assembly Workflow (Pen)

Invoke `stitch-ui-prompt-architect` and output a Stitch-ready prompt using this strict structure:

```text
[Context]
...

[Layout]
...

[Components]
...
```

### 5) Execution Workflow (Hand) — Tools Available

ALWAYS execute immediately (no confirmation loop):

1. Create project: `create_project`
2. Generate screen: `generate_screen_from_text`
3. List screens: `list_screens`
4. Get the target screen: `get_screen` (export screenshot + HTML assets)

### 6) Prompt-only Workflow — Tools Not Available

STOP execution. Do not fake results. Output only a copy-paste prompt for the user to run in Stitch.

## Output Patterns (Strict Templates)

Use these templates to keep outputs consistent.

### Template A — Tools Available (Execution Report)

ALWAYS use this exact template:

```markdown
# Stitch 设计交付

## 执行结果
- Project: projects/{id}
- Screen: {screenId}

## 资产导出
- Screenshot: {from get_screen output}
- HTML: {from get_screen output}

## 说明
- Prompt: 已按 `[Context] [Layout] [Components]` 结构执行（含必要约束与布局不变式）。
```

### Template B — Tools Not Available (Prompt Only)

ALWAYS use this exact template:

```text
[Context]
...

[Layout]
...

[Components]
...
```

## Anti-Patterns (Strict Prohibitions)
*   ⛔ **NO FAKE SUCCESS**: If you didn't get a real API response, do not say "Project Created".
*   ⛔ **NO APP SCAFFOLDING**: Do not invoke any external project scaffolding skills (e.g., `uniappx-project-creator`, `flutter-project-creater`, `react-native-project-creater`) and do not run scripts to create codebases.
*   ⛔ **NO CODING**: Do not write Vue/React/HTML code in this flow. This skill is for **Design Generation** only.
*   ⛔ **NO CONFUSION**: A "Stitch Project" is a design workspace, NOT a code repository.

## Keywords
orchestrator, design agent, ui designer, master skill, design flow, stitch pilot
