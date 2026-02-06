# Stitch Skills 索引

供 Agent 与人类按角色、阶段发现技能。完整说明见各技能目录下的 `SKILL.md`。阶段与全链路映射见 [pipeline-stage-to-stitch-skills.md](pipeline-stage-to-stitch-skills.md)。

**层级说明**：Orchestrator = 编排入口；Logic = 设计逻辑与提示；Execution = Stitch MCP 执行；Framework Spec = 框架设计约束（仅产出约束/前缀，不直接生成界面，需与 stitch-ui-prompt-architect 配合）；Conversion = Stitch 屏→代码；Knowledge = UED/规范参考；Meta = 技能工厂。

---

## 按层级与阶段

| name | description（一句话） | 层级 | 阶段（简写） |
|------|------------------------|------|----------------|
| stitch-ui-designer | 端到端编排：承接「Design X」请求，协调逻辑与 MCP。 | Orchestrator | 原型 |
| stitch-ui-design-spec-generator | 将需求/PRD 转为结构化设计规范（主题、设备、风格）。 | Logic | 需求→设计输入 |
| stitch-ui-prompt-architect | 从模糊想法或 Design Spec + 请求生成分段 Stitch 提示。 | Logic | 需求→设计输入、原型 |
| stitch-design-md | 分析 Stitch 项目，产出 DESIGN.md 设计系统说明。 | Logic | UI 说明、多页 |
| stitch-loop | 多页站点迭代：next-prompt → 生成 → 集成 → 更新 baton。 | Logic | 多页/站点 |
| stitch-ui-design-variants | 为同一屏生成 A/B 变体提示思路。 | Logic | 变体 |
| stitch-mcp-create-project | 创建新 Stitch 项目。 | Execution | 原型 |
| stitch-mcp-list-projects | 列出 Stitch 项目。 | Execution | 原型 |
| stitch-mcp-get-project | 获取项目元数据。 | Execution | 原型 |
| stitch-mcp-generate-screen-from-text | 从文本生成界面（Text-to-UI 核心）。 | Execution | 原型 |
| stitch-mcp-list-screens | 列出项目内所有屏。 | Execution | 原型 |
| stitch-mcp-get-screen | 获取单屏详情（HTML、截图等）。 | Execution | 原型 |
| stitch-ui-design-spec-bootstrap | Bootstrap 设计约束前缀 / CONTRACT；与 prompt-architect 配合。 | Framework Spec | 设计规范 |
| stitch-ui-design-spec-element-plus | Element Plus 设计约束前缀；与 prompt-architect 配合。 | Framework Spec | 设计规范 |
| stitch-ui-design-spec-layui | Layui-Vue 设计约束前缀；与 prompt-architect 配合。 | Framework Spec | 设计规范 |
| stitch-ui-design-spec-uview | uView 2 设计约束前缀；与 prompt-architect 配合。 | Framework Spec | 设计规范 |
| stitch-ui-design-spec-uviewpro | uView Pro 设计约束前缀；与 prompt-architect 配合。 | Framework Spec | 设计规范 |
| stitch-ui-design-spec-vant | Vant 4 设计约束前缀；与 prompt-architect 配合。 | Framework Spec | 设计规范 |
| stitch-react-components | Stitch 屏 → Vite/React 组件。 | Conversion | 前端代码 |
| stitch-shadcn-ui | shadcn/ui 集成与组件发现、定制；与 stitch-react-components 配合。 | Conversion | 前端代码 |
| stitch-vue-element-components | Stitch 屏 → Vue 3 + Element Plus。 | Conversion | 前端代码 |
| stitch-vue-bootstrap-components | Stitch 屏 → Vue 3 + Bootstrap。 | Conversion | 前端代码 |
| stitch-vue-layui-components | Stitch 屏 → Vue 3 + Layui-Vue。 | Conversion | 前端代码 |
| stitch-vue-vant-components | Stitch 屏 → Vue 3 + Vant 4 移动端。 | Conversion | 前端代码 |
| stitch-uview-components | Stitch 屏 → uni-app + Vue 2 + uView 2。 | Conversion | 前端代码 |
| stitch-uviewpro-components | Stitch 屏 → uni-app + Vue 3 + uView Pro。 | Conversion | 前端代码 |
| stitch-ued-guide | UED 指南、视觉词汇、设备约束、提示结构。 | Knowledge | 设计规范、交互 |
| stitch-remotion | Stitch 项目 → Remotion 讲解视频。 | — | 视频 |
| stitch-skill-creator | 创建新 Stitch 场景技能（SOP + 模板）。 | Meta | — |

---

## 参考

- 本库阶段→技能：[pipeline-stage-to-stitch-skills.md](pipeline-stage-to-stitch-skills.md)
- PRD 驱动流程：[prd-to-stitch-workflow.md](prd-to-stitch-workflow.md)
- 设计规范 vs 转代码技能对比：[skills-compare-design-spec-and-react.md](skills-compare-design-spec-and-react.md)
