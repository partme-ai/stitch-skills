# 与官方 Google Stitch Skills 的对照

本仓库**包含并强化** [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills)。每个官方技能都有**能力不低于官方**的本地等价物。

## 官方 → 本地映射（本地更强）

| 官方 | 本仓库（本地） | 为何本地更强 |
|----------|-------------------|------------------------|
| **design-md** | **stitch-design-md** | **更强**：DESIGN.md 包含 **Section 6**（Design System Notes for Stitch Generation）；官方仅 1–5 节。显式 stitch-mcp-* 命名（格式：stitch-mcp-<tool>，如 get_screen → stitch-mcp-get-screen）；与 stitch-ui-prompt-architect、stitch-loop 集成；引用框架设计规范。 |
| **enhance-prompt** | **stitch-ui-prompt-architect** | **更强**：双路径：(1) 模糊 → 增强提示（与官方一致）；(2) Design Spec + 请求 → 分段 Stitch 提示。另含框架契约前缀（uView、Element、Layui、Bootstrap、Vant）、KEYWORDS.md、以及 stitch-loop 的 next-prompt.md。 |
| **stitch-loop** | **stitch-loop** | **更强**：相同 baton/SITE.md；**Step 4.5** 可选 Chrome DevTools MCP 视觉校验；**编排方式**（CI/CD、人工介入、Agent 链、手动）；显式 stitch-mcp-* 命名；DESIGN.md Section 6；通过 stitch-ui-prompt-architect 提升提示质量。 |
| **react-components** | **stitch-react-components** | 相同拉取 + fetch 脚本 + 架构清单 + 组件模板；引用 stitch-mcp-* 做项目/屏幕发现；可选 DESIGN.md 对齐（stitch-design-md）。 |
| **remotion** | **stitch-remotion** | **更强**：相同走查流程；**常用模式**（幻灯片、功能高亮、用户流）；**旁白**与**动态文案提取**；**Remotion Skills** 与 **Remotion MCP** 链接；stitch-mcp-* 命名；DESIGN.md 用于叠加文案。 |
| **shadcn-ui** | **stitch-shadcn-ui** | **更强**：相同发现、安装、定制、blocks；**init 样式**（Vega、Nova、Maia、Lyra、Mira）；**自定义 registry**（get_project_registries、list_items_in_registries）；**校验与质量**清单；与 stitch-react-components、DESIGN.md 集成。 |

## 本仓库在官方基础上的新增

- **stitch-mcp-***：每个 MCP 工具对应一个技能；技能名 = MCP 工具名下划线改为连字符（如 generate_screen_from_text → stitch-mcp-generate-screen-from-text）。完整映射：[mcp-naming-convention.zh-CN.md](mcp-naming-convention.zh-CN.md)。
- **stitch-ui-design-spec-***：面向 Stitch 提示的框架设计契约（Bootstrap、Element Plus、Layui、uView、uView Pro、Vant）。
- **stitch-ui-designer**：端到端设计任务的主编排技能。
- **stitch-ui-design-spec-generator**：从模糊需求生成结构化规范（主题、设备、风格）。
- **stitch-skill-creator**：新场景技能的工厂。
- **stitch-ued-guide**：UED 指南与视觉词汇。
- **Stitch → 框架组件**：六个转换技能（Vue 3 + Element/Bootstrap/Layui/Vant，uni-app + uView/uView Pro），将 Stitch 屏幕转为可运行项目。
- **agents/stitch-ui-designer.md**：Stitch UI 工作流专用 agent。

## 何时用哪个

- **所有 Stitch 流程**：优先使用本仓库的 skills（stitch-*）。它们互相引用且共用同一 MCP；本地 prompt-architect 在双路径与框架契约上强于官方 enhance-prompt。
- **仅作参考**：需要额外示例或脚本时（如 react-components validate.js、remotion 模板），可查阅官方 [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills)。

Stitch 文档（提示词、设备类型、MCP）对双方均适用：[Stitch Learn](https://stitch.withgoogle.com/docs/learn/overview/)、[MCP Guide](https://stitch.withgoogle.com/docs/mcp/guide/)。

## 保持本地领先于官方

与 [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills) 同步时：

1. **对比 SKILL.md**：对每个官方技能（design-md、enhance-prompt、react-components、stitch-loop、remotion、shadcn-ui）对比本地等价物，确保保留或增强官方能力，并保留本地独有内容（MCP 技能名、框架契约、Section 6 等）。
2. **MCP 命名**：本地技能使用 **stitch-mcp-<tool>**（如 get_screen → stitch-mcp-get-screen；勿用 stitch-mcp-get-screen（旧式））。完整表：[mcp-naming-convention.zh-CN.md](mcp-naming-convention.zh-CN.md)。
3. **新官方技能**：若官方新增技能，在 `skills/` 下增加本地等价物，并在本表及 README 中说明。

设计规范与转换技能的角色说明（输入、输出、何时用哪个），见 [skills-compare-design-spec-and-react.zh-CN.md](skills-compare-design-spec-and-react.zh-CN.md)（中文）或 [skills-compare-design-spec-and-react.md](skills-compare-design-spec-and-react.md)（English）。
