# 技能对比：Design Spec 系 vs React Components

这组技能在 Stitch 工作流里职责不同：**Design Spec 系**负责「写什么提示 / 约束」，**stitch-react-components** 负责「把 Stitch 设计转成 React 代码」。下面按角色和差异说明。

---

## 一、角色总览

| 技能 | 角色 | 输入 | 输出 | 是否调用 Stitch MCP 生成 UI |
|------|------|------|------|-----------------------------|
| **stitch-ui-design-spec-generator** | 创意总监：把模糊需求结构化 | 自然语言需求 | 结构化 JSON（theme、device、style 等） | 否（只产出 Spec） |
| **stitch-ui-design-variants** | 变体生成：同一设计的多种方向 | 已有 Spec 或 Prompt | 多条替代 Prompt（A/B 风格） | 否（只产出 Prompt） |
| **stitch-ui-design-spec-bootstrap** | Bootstrap 5 / Vue 约束 | 用户需求 + 触发词 bootstrap | Hard constraints 前缀 或 CONTRACT_SELECTION_JSON | 否（给 prompt-architect 用） |
| **stitch-ui-design-spec-element-plus** | Element Plus / Vue3 约束 | 用户需求 + 触发词 element | 同上 | 否 |
| **stitch-ui-design-spec-layui** | Layui-Vue 约束 | 用户需求 + 触发词 layui | 同上 | 否 |
| **stitch-ui-design-spec-uview** | uView 2.0 / uni-app Vue2 约束 | 用户需求 + 触发词 uview | 同上 | 否 |
| **stitch-ui-design-spec-uviewpro** | uView Pro / uni-app Vue3 约束 | 用户需求 + 触发词 uviewpro | 同上 | 否 |
| **stitch-ui-design-spec-vant** | Vant 4 / Vue3 移动端约束 | 用户需求 + 触发词 vant | 同上 | 否 |
| **stitch-react-components** | 前端工程师：设计 → React 代码 | Stitch 项目 + Screen ID | React/Vite/TS 组件代码、mockData、校验 | 是（get_screen 取设计再转代码） |
| **stitch-vue-element-components** | 前端工程师：设计 → Vue3+Element Plus | Stitch 项目 + Screen ID | Vite Vue 3 .vue SFC、mockData、校验 | 是 |
| **stitch-vue-bootstrap-components** | 前端工程师：设计 → Vue3+Bootstrap | Stitch 项目 + Screen ID | Vite Vue 3 .vue SFC、mockData、校验 | 是 |
| **stitch-vue-layui-components** | 前端工程师：设计 → Vue3+Layui-Vue | Stitch 项目 + Screen ID | Vite Vue 3 .vue SFC、mockData、校验 | 是 |
| **stitch-vue-vant-components** | 前端工程师：设计 → Vue3+Vant 4 移动端 | Stitch 项目 + Screen ID | Vite Vue 3 .vue SFC、mockData、校验 | 是 |
| **stitch-uview-components** | 前端工程师：设计 → uni-app+uView 2 | Stitch 项目 + Screen ID | uni-app 页面、u-* 组件、校验 | 是 |
| **stitch-uviewpro-components** | 前端工程师：设计 → uni-app+uView Pro | Stitch 项目 + Screen ID | uni-app 页面、u-* 组件、rpx、校验 | 是 |

---

## 二、按职责分类

### 1. 通用「设计规范」逻辑（框架无关）

- **stitch-ui-design-spec-generator**  
  - **做什么**：把「一句话需求」转成**结构化设计规范**（主题、设备、模式、风格关键词等）。  
  - **输出**：JSON（如 `theme`, `deviceType`, `designMode`, `styleKeywords`）。  
  - **谁用**：下游 **stitch-ui-prompt-architect** 会结合这份 Spec + 用户请求，生成最终 Stitch 提示。  
  - **不同点**：不绑定任何 UI 框架，也不产出「组件级约束」或「前缀文本」。

- **stitch-ui-design-variants**  
  - **做什么**：在**已有设计 / 提示**基础上，生成**多版变体提示**（布局 / 风格 / 内容）。  
  - **输出**：多条 Stitch 可用的 Prompt（例如 3 种风格：暗色 / 亮色 / 高对比）。  
  - **谁用**：需要 A/B 或多种方案时，由编排或人工选一条再交给 Stitch 生成。  
  - **不同点**：只做「变体提示」，不做结构化 Spec，也不绑定框架。

### 2. 框架级「设计规范」约束（指定组件库）

- **stitch-ui-design-spec-bootstrap / element-plus / layui / uview / uviewpro / vant**  
  - **做什么**：为**某一个 UI 框架**输出 Stitch 可用的**硬约束**（设计 token + 组件契约）。  
  - **输出**：  
    - **Prefix 模式**：一段「Hard constraints prefix」文本，拼在 Stitch 提示的 `[Context]` 前面。  
    - **Selector 模式**：`CONTRACT_SELECTION_JSON_V1` + 按需组装的 Prompt（精修/美化现有屏时用）。  
  - **谁用**：**stitch-ui-prompt-architect** 在用户提到对应框架（如「element 风格」「uviewpro」）时，会调用对应 design-spec-* 拿到这段前缀或 JSON，再组装最终提示。  
  - **不同点**：  
    - 彼此**仅框架不同**（Bootstrap / Element Plus / Layui / uView / uView Pro / Vant），输出形态一致（前缀 或 JSON+Prompt）。  
    - 与 **stitch-ui-design-spec-generator** 不同：generator 只给「通用」JSON Spec，不给框架组件级约束；design-spec-* 只给「某框架」的约束，不给通用 theme/device 等 JSON。

### 3. 从设计到代码（执行层）

- **stitch-react-components**  
  - **做什么**：用 Stitch MCP（如 get_screen）拿到**已有 Stitch 设计**，转成 **Vite + React + TypeScript** 的组件代码（含 mockData、校验、Tailwind 等）。  
  - **输出**：源代码文件（组件、hooks、mockData）、可选校验结果。  
  - **不同点**：不产出「提示」或「Spec」，只产出 React 项目结构与代码；与 design-spec 无直接输入输出关系。

- **stitch-vue-*-components**（Vue 3 系）  
  - **stitch-vue-element-components**、**stitch-vue-bootstrap-components**、**stitch-vue-layui-components**、**stitch-vue-vant-components**  
  - **做什么**：用 get_screen 取回 Stitch 设计，按对应框架契约转成 **Vite + Vue 3 + 组件库** 的 .vue SFC、mockData、校验。  
  - **输出**：Vue 3 项目结构与代码；各技能仅目标栈不同（Element Plus / Bootstrap / Layui / Vant）。

- **stitch-uni-*-components**（uni-app 系）  
  - **stitch-uview-components**（Vue 2 + uView 2）、**stitch-uviewpro-components**（Vue 3 + uView Pro）  
  - **做什么**：用 get_screen 取回 Stitch 设计，按对应框架契约转成 **uni-app** 页面（pages/）、组件（u-*）、rpx、校验。  
  - **输出**：uni-app 项目结构与代码；与 design-spec-uview / design-spec-uviewpro 对齐契约。

---

## 三、典型流程里的位置

```
用户：「用 Stitch 做一套 Element 风格的后台登录页」
  → stitch-ui-design-spec-generator：得到通用 Spec（theme、device、styleKeywords）
  → stitch-ui-design-spec-element-plus：得到 Element Plus 的 Hard constraints 前缀
  → stitch-ui-prompt-architect：把 Spec + 前缀 + 登录页需求 合成最终 Stitch Prompt
  → stitch-mcp-screen-generate：调用 Stitch 生成界面

用户：「把刚才那个 Stitch 登录屏转成 React 项目」
  → stitch-react-components：get_screen 取设计 → 生成 React 组件 + mockData + 校验

用户：「把刚才那个 Stitch 登录屏转成 Element Plus 项目」
  → stitch-vue-element-components：get_screen 取设计 → 生成 Vue 3 + Element Plus .vue + mockData + 校验

用户：「把刚才那个 Stitch 首页转成 uni-app + uView Pro 项目」
  → stitch-uviewpro-components：get_screen 取设计 → 生成 uni-app 页面 + u-* 组件 + 校验
```

- **stitch-ui-design-variants**：在「已有设计/Prompt」上要多种风格时插入，产出多条 Prompt，再选一条去生成。

---

## 四、一句话区别

| 技能 | 一句话 |
|------|--------|
| **stitch-ui-design-spec-generator** | 把模糊需求变成**通用**设计规范 JSON（不绑定框架）。 |
| **stitch-ui-design-variants** | 在已有设计/Prompt 上生成**多条变体 Prompt**（A/B 风格）。 |
| **stitch-ui-design-spec-bootstrap** | 提供 **Bootstrap 5/Vue** 的 Stitch 硬约束（前缀或 JSON）。 |
| **stitch-ui-design-spec-element-plus** | 提供 **Element Plus/Vue3** 的 Stitch 硬约束。 |
| **stitch-ui-design-spec-layui** | 提供 **Layui-Vue** 的 Stitch 硬约束。 |
| **stitch-ui-design-spec-uview** | 提供 **uView 2.0 / uni-app Vue2** 的 Stitch 硬约束。 |
| **stitch-ui-design-spec-uviewpro** | 提供 **uView Pro / uni-app Vue3** 的 Stitch 硬约束。 |
| **stitch-ui-design-spec-vant** | 提供 **Vant 4 / Vue3 移动端** 的 Stitch 硬约束。 |
| **stitch-react-components** | 把 **Stitch 已生成的设计** 转成 **React 项目代码**。 |
| **stitch-vue-element-components** | 把 Stitch 设计转成 **Vue 3 + Element Plus** 项目代码。 |
| **stitch-vue-bootstrap-components** | 把 Stitch 设计转成 **Vue 3 + BootstrapVue** 项目代码。 |
| **stitch-vue-layui-components** | 把 Stitch 设计转成 **Vue 3 + Layui-Vue** 项目代码。 |
| **stitch-vue-vant-components** | 把 Stitch 设计转成 **Vue 3 + Vant 4**（移动端）项目代码。 |
| **stitch-uview-components** | 把 Stitch 设计转成 **uni-app + uView 2** 项目代码。 |
| **stitch-uviewpro-components** | 把 Stitch 设计转成 **uni-app + uView Pro** 项目代码。 |
