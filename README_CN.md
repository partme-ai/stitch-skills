<div align="center">

# Stitch Skills

**Stitch UI 生成的 Agent Skills 集合**

![Version](https://img.shields.io/badge/Version-1.0.0-blue)
![License](https://img.shields.io/badge/License-Apache%202.0-green)
![Skills](https://img.shields.io/badge/Skills-13-orange)

</div>

## 📖 简介

**Stitch Skills** 是一个 Agent Skills 集合，旨在通过 Stitch MCP 赋能 AI 智能体（如 Claude, Trae）自主设计和生成 UI 界面。它遵循 [Agent Skills 规范](https://agentskills.io/) 并提供了一套 "自循环" 的设计工作流。

## 🔗 官方资源 (Official Resources)

来自 Google Stitch 官方团队的核心文档：

*   **[概览 (Overview)](https://stitch.withgoogle.com/docs/learn/overview/)**: Stitch 能力介绍。
*   **[提示词指南 (Prompting)](https://stitch.withgoogle.com/docs/learn/prompting/)**: 编写高效设计提示词的最佳实践。
*   **[设备类型 (Device Types)](https://stitch.withgoogle.com/docs/learn/device-types/)**: 理解移动端、桌面端和 Web 布局。
*   **[设计模式 (Design Modes)](https://stitch.withgoogle.com/docs/learn/design-modes/)**: 标准模式 (Flash) 与 实验模式 (Pro) 的区别。
*   **[变体 (Variants)](https://stitch.withgoogle.com/docs/learn/variants/)**: 生成和管理设计变体。
*   **[控件 (Controls)](https://stitch.withgoogle.com/docs/learn/controls/)**: 使用交互式控件优化设计。
*   **[MCP 指南 (MCP Guide)](https://stitch.withgoogle.com/docs/mcp/guide/)**: Model Context Protocol 集成技术指南。

## 🔌 MCP 配置（想要真实执行必须做）

本仓库包含的是 **skills 与 tool schema**，并不包含 Stitch MCP Server 本体。

要让 Agent 真正创建项目/生成页面，你需要：

*   按官方文档安装与配置 Stitch MCP Server：https://stitch.withgoogle.com/docs/mcp/guide/
*   确认客户端暴露出 Stitch MCP 工具（本仓库 `docs/*.json` 定义的 tool 名称）：
    *   `create_project`
    *   `list_projects`
    *   `get_project`
    *   `generate_screen_from_text`
    *   `list_screens`
    *   `get_screen`

在部分客户端中，MCP 工具名可能带命名空间前缀，例如：

*   `mcp__<serverName>__create_project`
*   `mcp__<serverName>__generate_screen_from_text`

其中 `<serverName>` 必须与你 `mcpServers` 的配置名称一致。

## 🏗️ 架构

技能被组织成逻辑层，以实现自主的 "设计 -> 执行" 循环。

- **`stitch-ui-*`**: **大脑 (The Brain)**。负责设计逻辑、提示词工程和编排的技能。不产生外部 API 费用。
- **`stitch-mcp-*`**: **双手 (The Hands)**。Stitch MCP (Model Context Protocol) 的封装。负责执行实际的 API 调用。

```text
stitch-skills/
├── skills/
│   ├── stitch-ui-designer/          # [编排器] 主技能
│   ├── stitch-ui-design-spec-generator/ # [逻辑] 风格与规范逻辑
│   ├── stitch-ui-prompt-architect/      # [逻辑] 提示词工程
│   ├── stitch-mcp-project-create/   # [执行] 创建项目
│   ├── stitch-mcp-screen-generate/  # [执行] 生成 UI
│   ├── stitch-skill-creator/        # [元工具] 创建新技能
│   └── ...
├── docs/                            # API 规范
├── media/                           # 资源
├── LICENSE                          # Apache 2.0
└── README.md                        # 文档
```

## 📦 可用技能

### 编排器 (入口)
*   **`stitch-ui-designer`**: **主技能**。调用它来处理端到端的设计任务（例如 "设计一个登录页面"）。它会自动协调逻辑和执行技能。

### 逻辑与设计技能 (大脑)
*   **`stitch-ui-design-spec-generator`**: 分析模糊的用户请求，输出结构化的设计规范（主题、设备、风格）。
*   **`stitch-ui-prompt-architect`**: 将规范转换为详细、高质量的 Stitch Prompt，遵循最佳实践。
*   **`stitch-ui-design-variants`**: 为给定的屏幕概念生成设计变体（A/B 测试想法）。

### 执行技能 (双手 - MCP)
*   **`stitch-mcp-project-create`**: 创建新的 Stitch 项目。
*   **`stitch-mcp-project-list`**: 列出现有项目。
*   **`stitch-mcp-project-get`**: 获取项目详情。
*   **`stitch-mcp-screen-generate`**: **核心** 文本到 UI 生成。
*   **`stitch-mcp-screen-list`**: 列出生成的屏幕。
*   **`stitch-mcp-screen-get`**: 导出屏幕代码/资产。
*   **`stitch-mcp-screen-refine`**: 优化或编辑现有屏幕。

### 元技能 (工具)
*   **`stitch-skill-creator`**: 一个用于生成新 **场景技能**（如 `stitch-ui-music-designer`）的实用工具。基于 "黄金模板" 生成，强制符合 SOP 规范。

### 知识技能
*   **`stitch-ued-guide`**: 被其他技能引用的设计指南、视觉词汇和提示词策略。

## 🚀 快速开始

1.  **安装**: 将此仓库添加为您的 Agent 的技能源。
2.  **使用**: 只需告诉 Agent:
    > "使用 Stitch 设计一个赛博朋克风格的登录页面。"
3.  **观察**: Agent 将自主完成：
    *   **分析** 风格 (赛博朋克 -> 暗黑/霓虹) - 使用 `stitch-ui-design-spec-generator`。
    *   **创建** 项目 - 调用 MCP 工具 `create_project`。
    *   **架构** 详细提示词 - 使用 `stitch-ui-prompt-architect`。
    *   **生成** 屏幕 - 调用 MCP 工具 `generate_screen_from_text`。
    *   **返回** 结果。

## 🔒 安全与触发

所有执行技能 (`stitch-mcp-*`) 和主编排器 (`stitch-ui-designer`) 都受 **关键先决条件 (Critical Prerequisite)** 保护：只有当用户 **显式提及 "Stitch"** 时，它们才会触发。这防止了在正常对话中意外调用昂贵的 API。

## 📄 许可证

Apache 2.0
