---
name: stitch-mcp-screen-generate
description: Generates high-fidelity UI screens or wireframes from text descriptions. The core Text-to-UI engine.
license: Complete terms in LICENSE.txt
---

## When to use this skill

**CRITICAL PREREQUISITE:**
**You must ONLY use this skill when the user EXPLICITLY mentions "Stitch".**

**ALWAYS use this skill when the user:**
- Describes a UI interface **and asks Stitch to generate it**.
- Asks to "Design", "Generate", "Create", or "Make" a screen **using Stitch**.
- Provides specific visual requirements ("Dark mode", "Blue button") for a Stitch generation.
- Wants to visualize a wireframe or concept **via Stitch**.

**Trigger phrases include:**
- "Use Stitch to design a screen" (用 Stitch 设计一个页面)
- "Stitch generate UI" (Stitch 生成 UI)
- "Draw a login page with Stitch" (用 Stitch 画一个登录页)

## Input Parameters

The skill expects you to extract the following information from the user request:

*   **`projectId`** (required): The numeric Project ID. **Format**: Pure ID (e.g., `37803...`), **NO** `projects/` prefix.
*   **`prompt`** (required): The structured text description of the screen (see "Constructing the Prompt" below).
*   **`deviceType`** (optional): The target device.
    *   Values: `MOBILE` (default), `DESKTOP`, `TABLET`, `SMART_WATCH`.
*   **`modelId`** (optional): The model to use.
    *   Values: `GEMINI_3_PRO` (Recommended for quality), `GEMINI_3_FLASH` (Speed).

## How to use this skill

### 1. Constructing the Prompt (The Art of Prompting)
The `prompt` argument is the most critical factor for quality. Do not just pass the user's raw input. You **MUST** enrich it using the **Structure Strategy**:

`[Device] [Mode] [Screen Type]. [Style]. [Layout]. [Components].`

*   **Context**: "Mobile High-Fidelity login screen."
*   **Style**: "Cyberpunk aesthetic. Dark mode. Neon blue accents."
*   **Layout**: "Center-aligned vertical stack."
*   **Components**: "Glitch-effect Logo. Input fields with glowing borders. Primary 'Jack In' button."

### 2. Choosing Device Type (`deviceType`)
*   `MOBILE` (Default): Vertical layouts, ~375px width. Best for consumer apps.
*   `DESKTOP`: Horizontal layouts, ~1440px width. Best for SaaS, Dashboards, Landing Pages.
*   `TABLET`: Hybrid layouts.
*   `SMART_WATCH`: Tiny, compact layouts.

### 3. Choosing Model (`modelId`)
*   `GEMINI_3_PRO`: **Recommended**. High intelligence, better instruction following, superior aesthetics. Use for all complex/final designs.
*   `GEMINI_3_FLASH`: Faster, lower cost. Good for simple wireframes or rapid iteration.

## Best Practices

1.  **Detailed Components**: Don't just say "Form". Say "Form with Email, Password, and Eye toggle icon".
2.  **Color Precision**: Mention specific colors (e.g., "Emerald Green", "#FF5733") if the user specifies them.
3.  **Content Realism**: Ask for realistic text placeholders (e.g., "Welcome back, Alice" instead of "Lorem Ipsum").
4.  **Device Alignment**: Ensure the `prompt` description matches the `deviceType` (e.g., don't ask for a "Sidebar" on `MOBILE`).

## Output Handling

Returns a `design` object. You should:
1.  **Present the Screenshot**: Use the `screenshot.downloadUrl` to show the user the result.
2.  **Offer Code**: Mention that HTML/Figma exports are available via `stitch-mcp-screen-get`.

## Keywords

**English keywords:**
generate screen, design ui, create interface, make page, draw wireframe, text to ui, ui generation, stitch gen, mobile design, desktop design, dashboard, login, prompt engineering

**Chinese keywords (中文关键词):**
生成页面, 设计UI, 创建界面, 画图, 制作网页, 文本生成UI, 界面设计, 移动端设计, 桌面端设计, 仪表盘, 登录页, 线框图, 生成代码
