# Stitch MCP 技能命名约定

Stitch MCP 技能**以 MCP 工具名为准**命名，非随意命名。每个技能对应本仓库 `docs/*.json` 中定义的一个 MCP 工具。

## 规则

- **格式**：`stitch-mcp-<tool>` — 每个 MCP 工具对应一个技能；技能名由 `docs/*.json` 中的 MCP 工具 `name` **下划线改为连字符**（snake_case → kebab-case）得到。示例：`generate_screen_from_text` → **`stitch-mcp-generate-screen-from-text`**。见下表。

## MCP 工具 → 技能名映射

| MCP 工具名（`docs/*.json`） | 技能名 |
|--------------------------------|------------|
| `create_project` | `stitch-mcp-create-project` |
| `get_project` | `stitch-mcp-get-project` |
| `list_projects` | `stitch-mcp-list-projects` |
| `generate_screen_from_text` | `stitch-mcp-generate-screen-from-text` |
| `get_screen` | `stitch-mcp-get-screen` |
| `list_screens` | `stitch-mcp-list-screens` |

在其他技能或文档中引用 Stitch MCP 技能时，请使用上表中的名称。例如使用 **`stitch-mcp-generate-screen-from-text`**（对应 MCP 工具 `generate_screen_from_text`），不要使用 `stitch-mcp-screen-generate`。

## 参考

- MCP 工具 schema：本目录下 [docs/*.json](.)（如 [get_screen.json](get_screen.json)、[list_projects.json](list_projects.json)）。
- Stitch MCP 指南：https://stitch.withgoogle.com/docs/mcp/guide/
