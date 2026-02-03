---
name: stitch-ui-prompt-architect
description: Logic skill that constructs detailed, structure-aware Stitch Prompts based on Design Specs and User Request.
---

# UI Prompt Architect

**Constraint**: Only use this skill when the user explicitly mentions "Stitch" or when orchestrating a Stitch design task.

This skill acts as a **Senior UX Designer**. It merges the User Request and the Design Spec (from `stitch-ui-design-spec-generator`) into a final **Stitch-Ready Prompt**.

## Input
*   **User Request**: The functional requirement (e.g., "Login page with social auth").
*   **Design Spec**: The JSON output from `stitch-ui-design-spec-generator`.

## Output Format (Must)

Return a single prompt using this sectioned structure:

```text
[Context]
...

[Layout]
...

[Components]
...
```

## Construction Logic

### 1. Context & Style
Combine `deviceType`, `designMode`, `theme`, and `styleKeywords`.
*   *Example*: "Mobile High-Fidelity login screen. Cyberpunk aesthetic. Dark mode with neon blue accents."
*   *Wireframe Example*: "Mobile Wireframe sketch. Blueprint style. Monochrome."

### 1.5 Design Contract Prefix (Hard Constraints)

If the user request includes a named style constraint (e.g., "uview 风格"), prepend the corresponding **Hard constraints prefix** to the beginning of the prompt's `[Context]`.

Mapping:

*   `uview-pro`, `uviewpro` -> use `stitch-ui-design-spec-uviewpro` output as prefix
*   `uview`, `uview2` -> use `stitch-ui-design-spec-uview` output as prefix
*   `element`, `element-plus` -> use `stitch-ui-design-spec-element-plus` output as prefix
*   `vant`, `vant4` -> use `stitch-ui-design-spec-vant` output as prefix
*   `layui`, `layui-vue` -> use `stitch-ui-design-spec-layui` output as prefix
*   `bootstrap`, `bs-vue` -> use `stitch-ui-design-spec-bootstrap` output as prefix

### 1.6 Contract Selection JSON (Components + States)

When a named design system is present (e.g., `uview`), generate a `CONTRACT_SELECTION_JSON_V1` to decide which component contracts and UI state snippets to inject. Select only what is needed for the current screen.

Schema (fixed):

```json
{
  "version": "CONTRACT_SELECTION_JSON_V1",
  "designSystem": "uview2",
  "mode": "selector",
  "contracts": { "include": [] },
  "states": { "include": [] }
}
```

Assembly rules:

- `[Context]`: prepend design contract prefix; 对于美化/精修任务，额外注入“layout invariants”段以防布局漂移。
- `[Components]`: inject only snippets for `contracts.include` and `states.include`.

### 2. Layout Structure
Define the macro layout based on `deviceType`.
*   **Mobile**: Header -> Body (Stack) -> Footer (Nav/Action).
*   **Desktop**: Sidebar/TopNav -> Main Grid -> Widgets.

### 3. Component Details
Translate functional requirements into UI components.
*   "Login" -> Inputs (User/Pass), Button (Primary), Link (Forgot Pass).
*   "Dashboard" -> Cards (KPIs), Charts (Bar/Line), Tables (Data).

### 4. Content
Add specific text examples to make the design realistic.
*   Instead of "Text", use "Welcome back, Agent".

## Example Output
> "Mobile login screen for a Fintech App. Clean minimalist aesthetic. Light mode.
> Layout: Center-aligned vertical stack.
> Header: Brand logo 'PayFast' and 'Welcome' title.
> Form: Input field for 'Email' with mail icon. Input field for 'Password' with eye toggle.
> Actions: Full-width primary blue button 'Sign In'. 'Forgot Password?' link.
> Footer: 'Create Account' link."
