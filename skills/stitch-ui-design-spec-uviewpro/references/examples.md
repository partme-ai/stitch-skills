# Example: uView Pro Design Contract (Stitch Integration)

## Trigger Keywords

- Mention "Stitch" AND `uview pro` / `uview-pro` / `uviewpro` keywords.
- Examples (Chinese):
  - 使用 Stitch 和 uView Pro 风格设计一个电商首页
  - 使用 Stitch 和 uView Pro 风格重构个人设置页
- Examples (English):
  - Use Stitch in uView Pro style to design a mobile dashboard.
  - Create a login form using Stitch and uView Pro components.

## References

- Full Contract & Constraints: [references/contract.md](./contract.md)
- Official References: [references/official.md](./official.md)

## Expected Behavior

1. This skill outputs uView Pro hard constraints prefix (tokens/primary=#3c9cff/up- prefix, etc.).
2. The orchestrator appends it as `[Context]` prefix to the Stitch Prompt.
3. Subsequent generation uses `up-*` components, `uni.$u` utilities, and `rpx` units.
