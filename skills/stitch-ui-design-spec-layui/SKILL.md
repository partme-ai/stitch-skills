---
name: stitch-ui-design-spec-layui
description: Layui-Vue design spec tool for Stitch: outputs hard-constraints prefix or selector JSON + assembled prompt.
---

# Layui Design Spec (Layui-Vue / Vue 3.0)

**Constraint**: Only use this skill when the user explicitly mentions "Stitch".

## Purpose

This skill makes the Layui-Vue design spec executable in two modes:

1) **Prefix mode**: output a paste-ready **Hard constraints prefix** for Stitch `[Context]`.
2) **Selector mode**: output `CONTRACT_SELECTION_JSON_V1` and then an assembled Stitch prompt that injects only the required component/state snippets.

## Trigger Keywords

Prefer this skill when the user request includes any of:

- `layui`, `layui-vue`, `layui vue`

Chinese trigger keywords (only for triggering):

- `layui 风格`
- `layui admin`

## Source of Truth

- `references/contract.md`
- `references/examples.md`
- `references/official.md`

## Output (STRICT)

Decide the mode by the user intent:

- If the user asks for **beautify/polish/refine an existing screen**, or asks for **selector / JSON / contracts.include / states.include** → use **Selector mode**.
- Otherwise → use **Prefix mode**.

### Prefix mode

Return exactly one code block:

```text
[Hard constraints prefix...]
```

### Selector mode

Return exactly two code blocks, in this order, with no extra prose:

1) Contract selection JSON:

```json
{ ... }
```

2) Final Stitch prompt:

```text
[Context]
...

[Layout]
...

[Components]
...
```
