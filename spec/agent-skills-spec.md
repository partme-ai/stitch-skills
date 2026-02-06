# Agent Skills Spec

The canonical specification is at **[agentskills.io/specification](https://agentskills.io/specification)**. This file summarizes conventions used in this repository and optional fields aligned with [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills).

## Required

- **SKILL.md**: YAML frontmatter with `name` and `description`; body with when/how to use.
- **name**: Matches skill directory name; kebab-case; ≤64 chars.
- **examples/**: At least one usage example (gold-standard or scenario-based).
- **First line of body (Trae / simple-parser compatibility)**: The first non-empty line after the closing `---` MUST be a single-line short description (same as or a concise version of frontmatter `description`). This ensures tools that do not parse YAML frontmatter (e.g. some list/discovery UIs) still get a correct description when they use “first non-# line” as the skill description.

## Optional (this repo)

- **references/**: Deep-dive docs (contracts, official links, checklists). Load on demand to save context. (Upstream uses `resources/` for the same idea.)
- **scripts/**: Executable enforcers (validation, fetch, codegen). Use shebang, `set -e` for shell scripts; document inputs/outputs.
- **allowed-tools** (frontmatter): List of tool name patterns the agent may use when this skill is active (e.g. `"Read"`, `"Write"`, `"stitch*:*"`). **Include this block for consistent description recognition** in list/discovery UIs; use the same frontmatter structure as skills that are already recognized (e.g. `stitch-vue-element-components`). Omit only if you intentionally allow default tool access and do not rely on that UI. **Skills that call Stitch MCP** (e.g. stitch-design-md, stitch-ui-prompt-architect, stitch-mcp-*) must include the Stitch tool pattern in `allowed-tools` (e.g. `"stitch*:*"` or the client’s MCP prefix) so the agent is permitted to invoke those tools when the skill is active.
- **LICENSE.txt**: License for the skill content.

## Progressive disclosure

- Load only `name`/`description` for discovery.
- Load full SKILL.md when the skill is selected.
- Load `references/` or `examples/` only when needed. Keep SKILL.md under ~500 lines when possible.
