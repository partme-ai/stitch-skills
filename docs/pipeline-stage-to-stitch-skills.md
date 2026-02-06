# stitch-skills：本库阶段与技能映射

本文档仅列出 **本仓库（stitch-skills）** 在「需求→部署」全链路中负责的阶段及对应技能。完整全链路阶段与多仓库技能映射见 [full-stack-skills/docs/pipeline-stage-to-skills.md](../full-stack-skills/docs/pipeline-stage-to-skills.md)（同 workspace 内）或 full-stack-skills 仓库的 `docs/pipeline-stage-to-skills.md`。

---

## 本库负责的阶段与技能

| 阶段（简写） | 技能名 | 说明 |
|--------------|--------|------|
| **需求/PRD → 结构化设计输入** | stitch-ui-design-spec-generator, stitch-ui-prompt-architect | 从需求/PRD 提炼主题、设备、风格；生成 Stitch 可用的设计规范与提示词 |
| **设计规范 / 视觉与交互 DNA** | stitch-ui-design-spec-*（bootstrap, element-plus, layui, uview, uviewpro, vant）, stitch-ued-guide | 框架设计约束与 UED 指南、视觉词汇 |
| **UI 设计说明** | stitch-design-md | 从 Stitch 项目/屏产出 DESIGN.md，供后续生成与多页一致 |
| **原型（可交付界面）** | stitch-mcp-create-project, stitch-mcp-generate-screen-from-text, stitch-mcp-get-screen, stitch-mcp-list-projects, stitch-mcp-list-screens, stitch-mcp-get-project；编排：stitch-ui-designer | Stitch MCP 执行与编排 |
| **交互设计（规范与说明）** | stitch-ued-guide, stitch-ui-design-spec-* | 交互原则、组件约定、可访问性 |
| **前端代码（Stitch → 代码）** | stitch-react-components, stitch-shadcn-ui, stitch-vue-element-components, stitch-vue-bootstrap-components, stitch-vue-layui-components, stitch-vue-vant-components, stitch-uview-components, stitch-uviewpro-components | Stitch 屏转 Vue/React/uni-app 组件 |

---

## 辅助与元技能

| 阶段/用途 | 技能名 | 说明 |
|-----------|--------|------|
| 多页迭代 / 站点级 | stitch-loop, stitch-design-md | 多屏 baton、SITE.md、DESIGN.md 一致性 |
| 设计变体 | stitch-ui-design-variants | 为同一屏生成 A/B 变体思路 |
| 视频/演示 | stitch-remotion | Stitch 项目 → Remotion 讲解视频 |
| 技能工厂 | stitch-skill-creator | 创建新 Stitch 场景技能 |

---

## 上下游交接

- **上游**：PRD 或结构化需求来自 full-stack-doc（PRD 模板）、speckit-specify 等；本库不撰写 PRD，只消费 PRD 做设计输入。PRD 驱动流程见 [prd-to-stitch-workflow.md](prd-to-stitch-workflow.md)。
- **下游**：Stitch 产出（HTML/URL）→ 高保真 .pen 设计由 [pencil-skills](https://github.com/partme-ai/pencil-skills) 的 **pencil-design-from-stitch-html** 负责；本库仅负责 PRD→Stitch 原型。
