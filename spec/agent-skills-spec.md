# Agent Skills Spec

The canonical specification is at **[agentskills.io/specification](https://agentskills.io/specification)**. This file summarizes conventions used in this repository and optional fields aligned with [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills).

## Required

- **SKILL.md**: YAML frontmatter with `name` and `description`; body with when/how to use.
- **name**: Matches skill directory name; kebab-case; ≤64 chars.
- **examples/**: At least one usage example (gold-standard or scenario-based).

## Optional (this repo)

- **references/**: Deep-dive docs (contracts, official links, checklists). Load on demand to save context. (Upstream uses `resources/` for the same idea.)
- **scripts/**: Executable enforcers (validation, fetch, codegen). Use shebang, `set -e` for shell scripts; document inputs/outputs.
- **allowed-tools** (frontmatter): List of tool name patterns the agent may use when this skill is active (e.g. `"Read"`, `"Write"`, `"stitch*:*"`). Omit to allow default tool access.
- **LICENSE.txt**: License for the skill content.

## Progressive disclosure

- Load only `name`/`description` for discovery.
- Load full SKILL.md when the skill is selected.
- Load `references/` or `examples/` only when needed. Keep SKILL.md under ~500 lines when possible.
