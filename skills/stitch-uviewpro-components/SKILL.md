---
name: stitch-uviewpro-components
description: Convert Stitch designs into uni-app + Vue 3 + uView Pro pages and components. Uses Stitch MCP (get_screen) for retrieval; high-reliability fetch via scripts; enforces uni-app page structure and uView Pro (u-*) component contracts, rpx, script setup.
allowed-tools:
  - "stitch*:*"
  - "Bash"
  - "Read"
  - "Write"
  - "web_fetch"
---

# Stitch to uni-app + uView Pro Components

**Constraint**: Only use this skill when the user explicitly mentions "Stitch" and converting Stitch screens to **uni-app + Vue 3 + uView Pro** (pages/, components/, .vue or .uvue, u-* components).

You are a **frontend engineer** turning Stitch designs into clean, modular uni-app + uView Pro code. Use Stitch MCP (or **stitch-mcp-screen-get**) to retrieve screen metadata and HTML; use scripts and resources in this skill for reliable fetch and quality checks.

## Prerequisites

- Stitch MCP Server (https://stitch.withgoogle.com/docs/mcp/guide/)
- uni-app / HBuilderX or Vue CLI for uni-app (Vue 3)
- Stitch project and screen IDs (from **stitch-mcp-project-list**, **stitch-mcp-screen-list** if needed)

## Official Documentation

- **uView Pro (Vue 3)**: [Official](https://uviewpro.cn/) · [Guide](https://uviewpro.cn/zh/guide/intro.html) · [Components](https://uviewpro.cn/zh/components/intro.html) · [Tools](https://uviewpro.cn/zh/tools/intro.html) · [Layout / Templates](https://uviewpro.cn/zh/layout/intro.html)
- Full links and usage: [references/official.md](references/official.md)

## Retrieval and Networking

1. **Discover Stitch MCP prefix**: Run `list_tools` to find the prefix (e.g. `mcp_stitch__stitch:`).
2. **Fetch screen metadata**: Call `[prefix]:get_screen` with `projectId` and `screenId` (numeric IDs) to get design JSON, `htmlCode.downloadUrl`, `screenshot.downloadUrl`, dimensions, deviceType.
3. **High-reliability HTML download**: AI fetch tools can fail on Google Cloud Storage URLs. Use Bash to run the skill script:
   ```bash
   bash scripts/fetch-stitch.sh "<htmlCode.downloadUrl>" "temp/source.html"
   ```
   Ensure the URL is quoted.
4. **Visual reference**: Use `screenshot.downloadUrl` to confirm layout and details.

## Architectural Rules

- **Modular pages/components**: Split the design into pages under `pages/` and shared components under `components/`; avoid one giant page.
- **Logic isolation**: Use `<script setup>`; put event handlers and composables in appropriate modules.
- **Data decoupling**: Move static text, image URLs, and lists into `data/` or page data.
- **uView Pro only**: Use `u-*` components per [references/contract.md](references/contract.md) (u-row, u-col, u-navbar, u-button, u-form, u-input, etc.); use rpx for typography and spacing.
- **Project-specific**: Omit third-party license headers from generated pages/components.

## Execution Steps

1. **Environment**: Ensure uni-app project has uView Pro installed and configured (Vue 3, main.js, uni.scss).
2. **Data layer**: Create or update data sources (e.g. `data/mockData.js`) from the design content.
3. **Page drafting**: Use `resources/page-template.vue` as base; replace placeholder with real page name and uView Pro tags per contract.
4. **Wiring**: Register pages in `pages.json`; add tabBar or navigation as needed.
5. **Quality check**: Verify against `resources/architecture-checklist.md`; run in HBuilderX or CLI to confirm on simulator/device.

## Integration with This Repo

- **Get screen**: Use **stitch-mcp-screen-get** with projectId and screenId from **stitch-mcp-project-list** / **stitch-mcp-screen-list**.
- **Design spec**: If Stitch was generated with **stitch-ui-design-spec-uviewpro** constraints, map to uni-app pages and uView Pro components. If generic HTML, apply mapping rules from [references/contract.md](references/contract.md).
- **Design system**: If the project has DESIGN.md (from **stitch-design-md**), align colors and rpx spacing with that system when mapping to uView Pro tokens.

## Troubleshooting

- **Fetch errors**: Quote the URL in the bash command; ensure `scripts/fetch-stitch.sh` is executable.
- **Component mapping**: Follow [references/contract.md](references/contract.md) for layout (u-row, u-col, u-gap), forms (u-form, u-form-item, u-input), nav (u-navbar, u-tabs), list (u-swipe-action, u-list), feedback (u-toast, uni.$u).

## Keywords

**English:** Stitch, uni-app, uView Pro, Vue 3, u-button, u-navbar, rpx.  
**中文关键词：** Stitch、uni-app、uView Pro、组件。

## References

- [Contract (uView Pro mapping)](references/contract.md)
- [Component API (props/events quick reference)](api/component-api.md)
- [Official documentation](references/official.md)
- [Architecture checklist](resources/architecture-checklist.md)
- [Page template](resources/page-template.vue)
- [Stitch API / MCP](https://stitch.withgoogle.com/docs/mcp/guide/)
