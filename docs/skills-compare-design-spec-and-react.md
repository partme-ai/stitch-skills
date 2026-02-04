# Skill Comparison: Design Spec vs Conversion (React / Vue / uni-app)

These skills play different roles in the Stitch workflow: **Design Spec** skills define "what prompt/constraints to use"; **stitch-react-components** and the Vue/uni-app conversion skills turn Stitch designs into runnable code. Below: roles and differences.

---

## 1. Role Overview

| Skill | Role | Input | Output | Calls Stitch MCP to generate UI? |
|-------|------|-------|--------|-----------------------------------|
| **stitch-ui-design-spec-generator** | Creative director: structure vague requests | Natural language | Structured JSON (theme, device, style, etc.) | No (Spec only) |
| **stitch-ui-design-variants** | Variant generation: multiple directions for one design | Existing Spec or Prompt | Multiple alternative Prompts (A/B style) | No (Prompt only) |
| **stitch-ui-design-spec-bootstrap** | Bootstrap 5 / Vue constraints | User request + keyword bootstrap | Hard constraints prefix or CONTRACT_SELECTION_JSON | No (used by prompt-architect) |
| **stitch-ui-design-spec-element-plus** | Element Plus / Vue 3 constraints | User request + keyword element | Same | No |
| **stitch-ui-design-spec-layui** | Layui-Vue constraints | User request + keyword layui | Same | No |
| **stitch-ui-design-spec-uview** | uView 2.0 / uni-app Vue 2 constraints | User request + keyword uview | Same | No |
| **stitch-ui-design-spec-uviewpro** | uView Pro / uni-app Vue 3 constraints | User request + keyword uviewpro | Same | No |
| **stitch-ui-design-spec-vant** | Vant 4 / Vue 3 mobile constraints | User request + keyword vant | Same | No |
| **stitch-react-components** | Front-end: design → React code | Stitch project + Screen ID | React/Vite/TS components, mockData, validation | Yes (get_screen) |
| **stitch-vue-element-components** | Front-end: design → Vue 3 + Element Plus | Stitch project + Screen ID | Vite Vue 3 .vue SFC, mockData, validation | Yes |
| **stitch-vue-bootstrap-components** | Front-end: design → Vue 3 + Bootstrap | Stitch project + Screen ID | Same | Yes |
| **stitch-vue-layui-components** | Front-end: design → Vue 3 + Layui-Vue | Stitch project + Screen ID | Same | Yes |
| **stitch-vue-vant-components** | Front-end: design → Vue 3 + Vant 4 mobile | Stitch project + Screen ID | Same | Yes |
| **stitch-uview-components** | Front-end: design → uni-app + uView 2 | Stitch project + Screen ID | uni-app pages, u-* components, validation | Yes |
| **stitch-uviewpro-components** | Front-end: design → uni-app + uView Pro | Stitch project + Screen ID | uni-app pages, u-* components, rpx, validation | Yes |

---

## 2. By Responsibility

### 2.1 Generic design-spec logic (framework-agnostic)

- **stitch-ui-design-spec-generator**: Turns vague requests into structured design spec JSON (theme, device, styleKeywords, etc.). Output: JSON. Used by **stitch-ui-prompt-architect** to build the final Stitch prompt. Not tied to any UI framework.
- **stitch-ui-design-variants**: Generates multiple variant Prompts from existing design/Prompt (e.g. dark/light/high-contrast). Output: multiple Prompts. Used when A/B or multiple directions are needed.

### 2.2 Framework-level design-spec constraints

- **stitch-ui-design-spec-bootstrap / element-plus / layui / uview / uviewpro / vant**: Output Stitch-ready **hard constraints** (design tokens + component contract) for one UI framework. Output: Hard constraints prefix or CONTRACT_SELECTION_JSON + Prompt. Used by **stitch-ui-prompt-architect** when the user mentions that framework (e.g. "element style", "uviewpro"). Only the target framework differs; output shape is the same.

### 2.3 Design → code (execution)

- **stitch-react-components**: Uses Stitch MCP (e.g. get_screen) to get the design and produces React (Vite/TS) components, mockData, validation. No direct input/output with design-spec skills.
- **stitch-vue-*-components**: get_screen + framework contract → Vite Vue 3 .vue SFC. Only the target stack (Element Plus, Bootstrap, Layui, Vant) differs.
- **stitch-uview-components**, **stitch-uviewpro-components**: get_screen + contract → uni-app pages (u-* components, rpx). Aligned with design-spec-uview / design-spec-uviewpro.

---

## 3. Position in Typical Flows

```
User: "Use Stitch to build an Element-style admin login page"
  → stitch-ui-design-spec-generator: generic Spec (theme, device, styleKeywords)
  → stitch-ui-design-spec-element-plus: Element Plus hard constraints prefix
  → stitch-ui-prompt-architect: combine Spec + prefix + login request → final Stitch Prompt
  → stitch-mcp-generate-screen-from-text: call Stitch to generate UI

User: "Convert that Stitch login screen to a React project"
  → stitch-react-components: get_screen → React components + mockData + validation

User: "Convert that Stitch login screen to Element Plus"
  → stitch-vue-element-components: get_screen → Vue 3 + Element Plus .vue + mockData + validation

User: "Convert that Stitch home screen to uni-app + uView Pro"
  → stitch-uviewpro-components: get_screen → uni-app pages + u-* components + validation
```

**stitch-ui-design-variants**: Use when you want multiple styles from an existing design/Prompt; it outputs multiple Prompts; pick one and then generate.

---

## 4. One-line Summary

| Skill | One line |
|-------|----------|
| **stitch-ui-design-spec-generator** | Turn vague requests into **generic** design spec JSON (no framework). |
| **stitch-ui-design-variants** | Generate **multiple variant Prompts** from existing design/Prompt (A/B style). |
| **stitch-ui-design-spec-bootstrap** | Provide **Bootstrap 5/Vue** Stitch hard constraints (prefix or JSON). |
| **stitch-ui-design-spec-element-plus** | Provide **Element Plus/Vue 3** Stitch hard constraints. |
| **stitch-ui-design-spec-layui** | Provide **Layui-Vue** Stitch hard constraints. |
| **stitch-ui-design-spec-uview** | Provide **uView 2.0 / uni-app Vue 2** Stitch hard constraints. |
| **stitch-ui-design-spec-uviewpro** | Provide **uView Pro / uni-app Vue 3** Stitch hard constraints. |
| **stitch-ui-design-spec-vant** | Provide **Vant 4 / Vue 3 mobile** Stitch hard constraints. |
| **stitch-react-components** | Turn **Stitch design** into **React** project code. |
| **stitch-vue-element-components** | Turn Stitch design into **Vue 3 + Element Plus** project code. |
| **stitch-vue-bootstrap-components** | Turn Stitch design into **Vue 3 + BootstrapVue** project code. |
| **stitch-vue-layui-components** | Turn Stitch design into **Vue 3 + Layui-Vue** project code. |
| **stitch-vue-vant-components** | Turn Stitch design into **Vue 3 + Vant 4** (mobile) project code. |
| **stitch-uview-components** | Turn Stitch design into **uni-app + uView 2** project code. |
| **stitch-uviewpro-components** | Turn Stitch design into **uni-app + uView Pro** project code. |
