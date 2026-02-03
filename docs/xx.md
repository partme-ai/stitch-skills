## 怎么把现有前端体系变成 Stitch 约束（推荐路径）
### 1) 先定义“Token 约束”（最有效）
把你现有 tokens 提炼成 5 组硬规则（写到 prompt 顶部，像法律条文一样）：

- Color tokens ：primary/secondary/neutral + semantic（error/success/warn/info）
- Type scale ：H1/H2/H3/Body/Caption 的字号/行高/字重
- Spacing scale ：只能用 4/8/12/16/20/24/32/40…（禁止出现 13px 这种）
- Radius + Shadow ：圆角只能取 token，阴影只能取 token
- Motion ：过渡时长、easing 用 token（统一“精致感”） “粗糙”的主要来源就是 tokens 不一致：间距漂、字号体系混乱、阴影乱、圆角随机。
### 2) 再定义“组件契约”（把框架组件变成不可变形的组件规则）
为 Button / Input / Card / ListItem / Toast 等写契约：

- 尺寸：高度、padding、圆角
- 文案：字号、字重、对齐
- 状态：default/hover/pressed/disabled/loading/focus/error
- 细节：icon 尺寸、间距、错误提示位置
然后 prompt 里加一句强约束：

- “所有按钮必须遵循 Button Contract，不允许出现其他按钮样式”
- “所有输入框必须遵循 Input Contract，不允许新增输入框变体”
### 3) 固化“布局规则”（让对齐/密度看起来更专业）
移动端常用最强的 3 条：

- 左右安全边距固定（16 或 20）
- 所有主要元素对齐到同一列（不允许漂移）
- section 间距只用 spacing tokens（24/32/40）