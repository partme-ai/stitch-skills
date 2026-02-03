# Example: Element Plus Design Contract (Stitch Integration)

## Trigger Keywords

- Mention "Stitch" AND `element` / `element-plus` / `el-plus` keywords.
- Examples (Chinese):
  - 使用 Stitch 和 Element Plus 风格设计一个企业级后台管理系统
  - 使用 Stitch 和 Element Plus 风格重构登录页面
- Examples (English):
  - Use Stitch in Element Plus style to design a CRM dashboard.
  - Create a user settings form using Stitch and Element Plus.

## References

- Full Contract & Constraints: [references/contract.md](./contract.md)
- Official References: [references/official.md](./official.md)

## Expected Behavior

1. This skill outputs Element Plus hard constraints prefix (tokens/primary=#409EFF/radius/typography, etc.).
2. The orchestrator appends it as `[Context]` prefix to the Stitch Prompt.
3. Subsequent generation uses `el-*` components and the 24-column grid system.
