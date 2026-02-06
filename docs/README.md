# Stitch Skills — Documentation

This folder contains reference docs for the [stitch-skills](https://github.com/partme-ai/stitch-skills) repository.

| Doc | Description |
|-----|-------------|
| [pipeline-stage-to-stitch-skills.md](pipeline-stage-to-stitch-skills.md) | 本库在「需求→部署」全链路中的阶段与技能一览；完整映射见 full-stack-skills 的 `docs/pipeline-stage-to-skills.md`。 |
| [prd-to-stitch-workflow.md](prd-to-stitch-workflow.md) | PRD → Stitch 的输入契约（建议 PRD 结构）与推荐流程（spec-generator → framework spec → prompt-architect → MCP）。 |
| [skills-index.md](skills-index.md) | 所有 stitch-* 技能表格式索引（name / description / 层级 / 阶段），便于按角色与阶段发现技能。 |
| [related-upstream.md](related-upstream.md) | Alignment with official Google stitch-skills; official vs local mapping; what this repo adds; keeping local ahead. **中文:** [related-upstream.zh-CN.md](related-upstream.zh-CN.md). |
| [mcp-naming-convention.md](mcp-naming-convention.md) | MCP tool name → skill name (e.g. get_screen → stitch-mcp-get-screen). **中文:** [mcp-naming-convention.zh-CN.md](mcp-naming-convention.zh-CN.md). |
| [skills-compare-design-spec-and-react.md](skills-compare-design-spec-and-react.md) | Design Spec skills vs conversion skills (roles, inputs, outputs, when to use). **中文:** [skills-compare-design-spec-and-react.zh-CN.md](skills-compare-design-spec-and-react.zh-CN.md). |
| [color-prompt-guide.md](color-prompt-guide.md) | Ready-to-use color/theme prompts for Stitch Context & Style (8 palettes with hex; source: [AI配色提示词-UI配色指南](https://mp.weixin.qq.com/s/1SDFd7ZOPkbhpvHsmTJQjQ)). |
| [登录_PRD.md](登录_PRD.md) | Sample PRD (login/register) used in examples. |
| [xx.md](xx.md) | 将现有前端体系变为 Stitch 约束的推荐路径（中文，进阶）. |

MCP tool schemas (for client integration): `create_project.json`, `get_project.json`, `list_projects.json`, `generate_screen_from_text.json`, `get_screen.json`, `list_screens.json`.
