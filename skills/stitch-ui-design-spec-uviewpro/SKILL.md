# uView Pro Design Specification (Stitch Integration)

## 1. Skill Identity

- **Name**: `stitch-ui-design-spec-uviewpro`
- **Description**: Provides design constraints and style tokens for uView Pro (Vue 3 / uni-app) to ensure generated UIs are consistent with the uView Pro design system.
- **Trigger**: User mentions "uView Pro", "uview-pro", "uviewpro".
- **Role**: `Spec Provider` (Passive). This skill does not execute actions but provides `[Context]` to the prompt.

## 2. Trigger Logic

- **Pattern**: `(Stitch) + (uView Pro | uview-pro | uviewpro)`
- **Mapping**: `uview-pro`, `uviewpro`, `uview pro` -> use `stitch-ui-design-spec-uviewpro`

## 3. Output Behavior

### Prefix mode (Default)
When the user asks to "Design a screen using uView Pro style", this skill injects a **Hard Constraint Block** at the beginning of the prompt.

**Return exactly one code block:**

```markdown
[Context: Design System Constraints]
- **Framework**: uView Pro (Vue 3 / uni-app).
- **Design Tokens**:
  - **Colors**: Primary=#3c9cff, Success=#5ac725, Warning=#f9ae3d, Danger=#f56c6c, Info=#909399.
  - **Typography**: Base size 28rpx (14px). Font weights: 400 (normal), 700 (bold).
  - **Spacing**: Use `u-margin-*`, `u-padding-*` classes or `gap` prop.
  - **Radius**: Base=8rpx (4px), Large=16rpx (8px), Circle=9999px.
  - **Shadows**: Minimal usage.
- **Component Contracts**:
  - **Buttons**: Use `<up-button type="primary">`. Note the `up-` prefix.
  - **Grid**: Use `<up-row>` and `<up-col>`.
  - **Forms**: Use `<up-form>`, `<up-form-item>`, `<up-input>`, `<up-upload>`.
  - **Navigation**: Use `<up-navbar>`, `<up-tabbar>`.
  - **Feedback**: Use `<up-toast>`, `<up-modal>`, `<up-popup>`.
  - **Icons**: Use `<up-icon name="photo">`.
- **Layout Invariants**:
  - Use `rpx` for responsive sizing on mobile.
  - Always wrap pages in a root `<view>` or `<up-page>` if available.
  - Use `uni.$u.xxx` for JS utilities (e.g., `uni.$u.toast()`).
```

### Selector mode (Refinement)
When the user asks to "Fix the button style" or "Make it more uView Pro-like", inject specific component rules.

**Return JSON:**
```json
{
  "target_component": "up-button",
  "rules": [
    "Use 'type' prop (primary, success, etc.)",
    "Use 'shape' prop (circle, square)",
    "Use 'size' prop (large, normal, small, mini)"
  ]
}
```

## 4. References

- [Contract Definitions](./references/contract.md)
- [Official Documentation](./references/official.md)
- [Usage Examples](./references/examples.md)
