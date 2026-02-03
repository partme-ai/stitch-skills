# Bootstrap-Vue Design Specification (Stitch Integration)

## 1. Skill Identity

- **Name**: `stitch-ui-design-spec-bootstrap`
- **Description**: Provides design constraints and style tokens for BootstrapVue (Vue 3 + Bootstrap 5/4 style) to ensure generated UIs are consistent with the Bootstrap design system.
- **Trigger**: User mentions "Bootstrap", "BootstrapVue", "bs-vue".
- **Role**: `Spec Provider` (Passive). This skill does not execute actions but provides `[Context]` to the prompt.

## 2. Trigger Logic

- **Pattern**: `(Stitch) + (Bootstrap | BootstrapVue | bs-vue)`
- **Mapping**: `layui`, `layui-vue`, `layui vue` -> use `stitch-ui-design-spec-layui`
- **Mapping**: `bootstrap`, `bootstrap-vue`, `bs-vue` -> use `stitch-ui-design-spec-bootstrap`

## 3. Output Behavior

### Prefix mode (Default)
When the user asks to "Design a screen using Bootstrap style", this skill injects a **Hard Constraint Block** at the beginning of the prompt.

**Return exactly one code block:**

```markdown
[Context: Design System Constraints]
- **Framework**: BootstrapVue (Vue 3 compatible).
- **Design Tokens**:
  - **Colors**: Primary=#0d6efd (Bootstrap Blue), Secondary=#6c757d, Success=#198754, Danger=#dc3545, Warning=#ffc107, Info=#0dcaf0.
  - **Typography**: Font-family: system-ui, -apple-system, "Segoe UI", Roboto. Base size: 16px (1rem).
  - **Spacing**: STRICTLY use Bootstrap utility classes (m-*, p-*, gap-*). Scale: 0.25rem (4px) per unit.
  - **Radius**: $border-radius: 0.375rem (6px). Use `rounded`, `rounded-3`.
  - **Shadows**: `shadow-sm`, `shadow`, `shadow-lg`.
- **Component Contracts**:
  - **Buttons**: Use `<b-button variant="...">`. DO NOT use raw `<button class="btn ...">`.
  - **Grid**: Use `<b-container>`, `<b-row>`, `<b-col>`. DO NOT use raw `div.container`.
  - **Forms**: Use `<b-form-group>`, `<b-form-input>`, `<b-form-select>`.
  - **Cards**: Use `<b-card>`, `<b-card-header>`, `<b-card-body>`.
  - **Icons**: Use Bootstrap Icons via `<b-icon icon="...">`.
- **Layout Invariants**:
  - Always use the Grid system for layout structure.
  - Mobile-first responsive classes (e.g., `col-12 col-md-6`).
```

### Selector mode (Refinement)
When the user asks to "Fix the button style" or "Make it more Bootstrap-like", inject specific component rules.

**Return JSON:**
```json
{
  "target_component": "b-button",
  "rules": [
    "Use 'variant' prop instead of style attribute",
    "Use 'size' prop (sm, lg) for scaling",
    "Avoid custom CSS if utility classes can achieve the look"
  ]
}
```

## 4. References

- [Contract Definitions](./references/contract.md)
- [Official Documentation](./references/official.md)
- [Usage Examples](./references/examples.md)
