# Stitch MCP Skill Naming Convention

Stitch MCP skills are **named after the MCP tool names**, not arbitrarily. Each skill corresponds to one MCP tool defined in this repo’s `docs/*.json` schema files.

## Rule

- **Format**: `stitch-mcp-{resource}-{action}` (kebab-case).
- **Source**: The MCP tool `name` field in `docs/*.json` (e.g. `get_screen`, `create_project`).
- **Mapping**: MCP tool name (snake_case) is converted to skill name by taking resource and action:  
  `{resource}_{action}` or `{action}_{resource}` → `stitch-mcp-{resource}-{action}`.

## MCP Tool → Skill Name Mapping

| MCP tool name (`docs/*.json`) | Skill name |
|--------------------------------|------------|
| `create_project` | `stitch-mcp-project-create` |
| `get_project` | `stitch-mcp-project-get` |
| `list_projects` | `stitch-mcp-project-list` |
| `generate_screen_from_text` | `stitch-mcp-screen-generate` |
| `get_screen` | `stitch-mcp-screen-get` |
| `list_screens` | `stitch-mcp-screen-list` |

When referring to Stitch MCP skills in other skills or docs, use the names above. For example, use **`stitch-mcp-screen-get`** (from MCP tool `get_screen`), not `stitch-mcp-get-screen`.

## References

- MCP tool schemas: [docs/*.json](.) (e.g. [get_screen.json](get_screen.json), [list_projects.json](list_projects.json)).
- Stitch MCP Guide: https://stitch.withgoogle.com/docs/mcp/guide/
