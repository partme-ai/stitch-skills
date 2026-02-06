# PRD → Stitch 工作流：输入契约与推荐流程

本文档定义「可被 Stitch 技能消费的 PRD」建议结构，以及从 PRD 到 Stitch 原型与设计的推荐步骤。具备下列结构的 PRD 可走 **PRD 驱动流程**；其他 PRD 仍可通过自然语言或摘要被本库技能使用。

---

## 一、输入契约：可被 Stitch 消费的 PRD 建议结构

不必强制所有 PRD 都符合；但具备以下段落时，Agent 可稳定地按 PRD 驱动流程执行。

| 段落 | 用途 |
|------|------|
| **功能概述 / 核心功能** | 提炼产品类型、业务域（如医疗/金融/生活），供 stitch-ui-design-spec-generator 推断主题、色调、设备。 |
| **页面/屏幕列表** | 明确要生成的屏（如登录页、注册页、首页），驱动 stitch-mcp-generate-screen-from-text 的调用次数与顺序。 |
| **关键交互** | 用于 stitch-ui-prompt-architect 与 stitch-ued-guide：导航方式、表单步骤、状态（加载/错误）。 |
| **非功能需求中的视觉/主题偏好** | 性能、安全以外的「风格」「品牌」「多端」等，供 design spec 与 prompt 使用。 |

**上游来源**：PRD 可来自 [full-stack-skills](https://github.com/partme-ai/full-stack-skills) 的 full-stack-doc（PRD 模板）、[speckit-agent-skills](https://github.com/dceoy/speckit-agent-skills) 的 speckit-specify 产出等。衔接方式：用户提供 **文件路径**（如 `docs/登录_PRD.md`）或 **粘贴 PRD 内容**；Agent 读取后按本流程执行。

---

## 二、推荐流程（PRD 驱动）

1. **输入**：PRD 文档路径或 PRD 正文。
2. **结构化设计规范**：使用 **stitch-ui-design-spec-generator**，从 PRD 提炼：功能概述 + 页面列表 → 主题（LIGHT/DARK）、设备（MOBILE/DESKTOP 等）、风格关键词、设计模式（WIREFRAME/HIGH_FIDELITY）。输入可为「一句话需求」或 PRD 摘要/片段。
3. **选定框架约束**：根据技术栈选用 **stitch-ui-design-spec-***（如 uviewpro、element-plus、bootstrap、vant、layui、uview），得到该框架的硬约束前缀与 CONTRACT 片段。
4. **生成 Stitch 提示**：使用 **stitch-ui-prompt-architect**，将「设计规范 + 框架约束 + 具体页面/交互」合成为分段的 Stitch 提示（Context / Layout / Components / Content）。
5. **执行 Stitch MCP**：**stitch-mcp-create-project**（如需新项目）→ **stitch-mcp-generate-screen-from-text**（按页面列表逐屏生成，或按需）→ **stitch-mcp-get-screen** 获取 HTML/截图。
6. **可选**：多页一致性时使用 **stitch-design-md** 产出 DESIGN.md，再用 **stitch-loop** 迭代后续屏；需要 UED/可访问性时引用 **stitch-ued-guide**。
7. **下游**：若需从 Stitch 产出做高保真 .pen 设计，交给 [pencil-skills](https://github.com/partme-ai/pencil-skills) 的 **pencil-design-from-stitch-html**（本库不实现 Stitch HTML→.pen）。

---

## 三、何时用哪些技能

- **stitch-ued-guide**：需要布局/风格术语、设备约束、可访问性表述或统一视觉词汇时，与 stitch-ui-prompt-architect 配合使用。
- **stitch-design-md**：已有 Stitch 项目且希望后续屏与现有设计语言一致时，先分析项目产出 DESIGN.md，再用于 prompt-architect 或 stitch-loop。
- **pencil-design-from-stitch-html**：当需求是「Stitch 原型 → 高保真 .pen 设计稿」时，在 Stitch 生成完成后由 pencil-skills 承接。

---

## 四、参考

- 本库阶段与技能一览：[pipeline-stage-to-stitch-skills.md](pipeline-stage-to-stitch-skills.md)
- 示例 PRD： [登录_PRD.md](登录_PRD.md)
- 全链路阶段映射：full-stack-skills 的 [pipeline-stage-to-skills.md](../full-stack-skills/docs/pipeline-stage-to-skills.md)
