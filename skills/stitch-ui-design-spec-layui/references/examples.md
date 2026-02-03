# Example: Layui-Vue Design Contract (Stitch Integration)

## Trigger Keywords

- Mention "Stitch" AND `layui` / `layui-vue` keywords.
- Examples (Chinese):
  - 使用 Stitch 和 Layui 风格设计一个后台管理系统的仪表盘
  - 使用 Stitch 和 layui 风格 实现 `docs/登录_PRD.md` 文档要求的设计工作
- Examples (English):
  - Use Stitch in Layui-Vue style to design a Dashboard.

## References

- Full Contract & Constraints: [references/contract.md](./contract.md)
- Official References: [references/official.md](./official.md)

## Expected Behavior

1. This skill outputs Layui hard constraints prefix (tokens/radius=2px/primary=#16baaa, etc.).
2. The orchestrator appends it as `[Context]` prefix to the Stitch Prompt.
3. Subsequent generation / refinement maintains consistency with Layui style.
