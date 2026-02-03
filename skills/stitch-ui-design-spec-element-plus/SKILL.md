# Element Plus Design Specification (Stitch Integration)

## 1. Skill Identity

- **Name**: `stitch-ui-design-spec-element-plus`
- **Description**: Provides design constraints and style tokens for Element Plus (Vue 3) to ensure generated UIs are consistent with the Element Plus design system.
- **Trigger**: User mentions "Element Plus", "Element", "el-plus", "Element UI".
- **Role**: `Spec Provider` (Passive). This skill does not execute actions but provides `[Context]` to the prompt.

## 2. Trigger Logic

- **Pattern**: `(Stitch) + (Element Plus | Element | el-plus | Element UI)`
- **Mapping**: `element`, `element-plus`, `el-plus`, `element-ui` -> use `stitch-ui-design-spec-element-plus`

## 3. Output Behavior

### Prefix mode (Default)
When the user asks to "Design a screen using Element Plus style", this skill injects a **Hard Constraint Block** at the beginning of the prompt.

**Return exactly one code block:**

```markdown
[Context: Design System Constraints]
- **Framework**: Element Plus (Vue 3).
- **Design Tokens**:
  - **Colors**: Primary=#409EFF (Brand Blue), Success=#67C23A, Warning=#E6A23C, Danger=#F56C6C, Info=#909399.
  - **Typography**: Font-family: "Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", Arial, sans-serif.
  - **Spacing**: Default layout spacing 20px. Use `<el-space>` or padding/margin utilities.
  - **Radius**: Base=4px, Small=2px, Round=20px.
  - **Shadows**: `var(--el-box-shadow-light)`, `var(--el-box-shadow)`.
- **Component Contracts**:
  - **Buttons**: Use `<el-button type="...">`.
  - **Grid**: Use `<el-row :gutter="20">` and `<el-col :span="...">`.
  - **Forms**: Use `<el-form>`, `<el-form-item>`, `<el-input>`, `<el-select>`.
  - **Cards**: Use `<el-card shadow="hover">` with `#header`.
  - **Icons**: Use `@element-plus/icons-vue`. Usage: `<el-icon><Plus /></el-icon>`.
- **Layout Invariants**:
  - Always use `el-container`, `el-header`, `el-aside`, `el-main`, `el-footer` for full-page layouts.
  - Use `el-row` / `el-col` for responsive grids (24-column system).
```

### Selector mode (Refinement)
When the user asks to "Fix the button style" or "Make it more Element-like", inject specific component rules.

**Return JSON:**
```json
{
  "target_component": "el-button",
  "rules": [
    "Use 'type' prop (primary, success, danger) for coloring",
    "Use 'plain' prop for outlined style",
    "Use 'round' or 'circle' for shape"
  ]
}
```

## 4. References

- [Contract Definitions](./references/contract.md)
- [Official Documentation](./references/official.md)
- [Usage Examples](./references/examples.md)
