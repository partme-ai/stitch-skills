# Stitch MCP Skill Naming Convention

Stitch MCP skills are **named after the MCP tool names**, not arbitrarily. Each skill corresponds to one MCP tool defined in this repo’s `docs/*.json` schema files.

## Rule

- **Format**: `stitch-mcp-<tool>` — one skill per MCP tool; the skill name is the MCP tool `name` from `docs/*.json` with **underscores replaced by hyphens** (snake_case → kebab-case). Example: `generate_screen_from_text` → **`stitch-mcp-generate-screen-from-text`**. See the mapping table below.

## MCP Tool → Skill Name Mapping

| MCP tool name (`docs/*.json`) | Skill name |
|--------------------------------|------------|
| `create_project` | `stitch-mcp-create-project` |
| `get_project` | `stitch-mcp-get-project` |
| `list_projects` | `stitch-mcp-list-projects` |
| `generate_screen_from_text` | `stitch-mcp-generate-screen-from-text` |
| `get_screen` | `stitch-mcp-get-screen` |
| `list_screens` | `stitch-mcp-list-screens` |

When referring to Stitch MCP skills in other skills or docs, use the names above. For example, use **`stitch-mcp-generate-screen-from-text`** (from MCP tool `generate_screen_from_text`), not `stitch-mcp-screen-generate`.

## References

- MCP tool schemas: [docs/*.json](.) (e.g. [get_screen.json](get_screen.json), [list_projects.json](list_projects.json)).
- Stitch MCP Guide: https://stitch.withgoogle.com/docs/mcp/guide/
