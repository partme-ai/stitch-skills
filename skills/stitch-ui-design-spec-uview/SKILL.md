---
name: stitch-ui-design-spec-uview
description: uView 2.0 design spec tool for Stitch (uni-app / Vue2): outputs hard-constraints prefix or selector JSON + assembled prompt.
---

# uView Design Spec (uView 2.0 / uni-app / Vue2)

**Constraint**: Only use this skill when the user explicitly mentions "Stitch".

## Purpose

This skill makes the uView 2.0 design spec executable in two modes:

1) **Prefix mode**: output a paste-ready **Hard constraints prefix** for Stitch `[Context]`.
2) **Selector mode**: output `CONTRACT_SELECTION_JSON_V1` and then an assembled Stitch prompt that injects only the required component/state snippets.

## Trigger Keywords

Prefer this skill when the user request includes any of:

- `uview`, `uview2`, `uview2.0`, `u-view`

**Negative Constraint**: If the user says "uView Pro" or "uviewpro", DO NOT use this skill. Use `stitch-ui-design-spec-uviewpro` instead.

Chinese trigger keywords (only for triggering):

- `uview 风格`
- `美化`
- `优化`

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
