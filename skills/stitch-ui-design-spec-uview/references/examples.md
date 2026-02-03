# Example: uView 2.0 Design Contract (Stitch Integration)

## Trigger Keywords

- Mention "Stitch" AND `uview` keywords.
- Examples (Chinese):
  - 使用 Stitch 和 uview 风格 实现 `docs/登录_PRD.md` 文档要求的设计工作
- Examples (English):
  - Use Stitch in uView 2.0 style to design a mobile Login screen.

## References

- Full Contract & Constraints: [references/contract.md](./contract.md)
- Official References: [references/official.md](./official.md)

## Expected Behavior

1. This skill outputs uView hard constraints prefix (tokens/spacing/type/radius/shadows, etc.).
2. The orchestrator appends it as `[Context]` prefix to the Stitch Prompt.
3. Subsequent generation / refinement maintains consistency with uView style and avoids layout drift.
