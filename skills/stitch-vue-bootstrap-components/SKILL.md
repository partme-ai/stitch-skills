---
name: stitch-vue-bootstrap-components
description: Convert Stitch designs into modular Vite/Vue 3 + BootstrapVue (or BootstrapVueNext) components. Uses [BootstrapVue Vue 3](https://bootstrap-vue.org/vue3) support; Stitch MCP (get_screen) for retrieval; high-reliability fetch via scripts; enforces Vue SFC structure and Bootstrap component contracts (b-container, b-row, b-button, etc.).
allowed-tools:
  - "stitch*:*"
  - "Bash"
  - "Read"
  - "Write"
  - "web_fetch"
---

# Stitch to Vue 3 + Bootstrap Components

**Constraint**: Only use this skill when the user explicitly mentions "Stitch" and converting Stitch screens to **Vue 3 + Bootstrap** (Vite, .vue SFC, [BootstrapVue Vue 3](https://bootstrap-vue.org/vue3) or BootstrapVueNext).

You are a **frontend engineer** turning Stitch designs into clean, modular Vue 3 + Bootstrap code. Use Stitch MCP (or **stitch-mcp-screen-get**) to retrieve screen metadata and HTML; use scripts and resources in this skill for reliable fetch and quality checks. Target stack: Vue 3 + [BootstrapVue Vue.js 3 Support](https://bootstrap-vue.org/vue3) (@vue/compat) or BootstrapVueNext (Bootstrap 5 + Vue 3).

## Prerequisites

- Stitch MCP Server (https://stitch.withgoogle.com/docs/mcp/guide/)
- Node.js and npm (for Vite/Vue 3 project)
- Stitch project and screen IDs (from **stitch-mcp-project-list**, **stitch-mcp-screen-list** if needed)

## Official Documentation

- **Bootstrap Vue**: [Official](https://bootstrap-vue.org) · [Vue 3 support](https://bootstrap-vue.org/vue3) · [Docs](https://bootstrap-vue.org/docs) · [Components](https://bootstrap-vue.org/docs/components) · [GitHub](https://github.com/bootstrap-vue/bootstrap-vue)
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

- **Modular components**: Split the design into separate .vue files; avoid one giant SFC.
- **Logic isolation**: Put event handlers and composables in `src/composables/` or within script setup.
- **Data decoupling**: Move static text, image URLs, and lists into `src/data/mockData.js` (or .ts).
- **Bootstrap components only**: Use `<b-container>`, `<b-row>`, `<b-col>`, `<b-button>`, `<b-card>`, etc. per [references/contract.md](references/contract.md); do not use raw `<button class="btn">` when `<b-button>` applies.
- **Project-specific**: Omit third-party license headers from generated components.

## Execution Steps

1. **Environment**: If the project has no `node_modules`, run `npm install`.
2. **Data layer**: Create `src/data/mockData.js` from the design content.
3. **Component drafting**: Use `resources/component-template.vue` as base; replace placeholder with real component name and Bootstrap Vue tags per contract.
4. **Wiring**: Update the app entry (e.g. `App.vue` or router) to render the new components.
5. **Quality check**: Verify against `resources/architecture-checklist.md`; run `npm run dev` to confirm visually.

## Integration with This Repo

- **Get screen**: Use **stitch-mcp-screen-get** with projectId and screenId from **stitch-mcp-project-list** / **stitch-mcp-screen-list**.
- **Design spec**: If Stitch was generated with **stitch-ui-design-spec-bootstrap** constraints, map to Vue SFC and Bootstrap Vue components. If generic HTML, apply mapping rules from [references/contract.md](references/contract.md).
- **Design system**: If the project has DESIGN.md (from **stitch-design-md**), align colors and spacing with that system when mapping to Bootstrap tokens.

## Troubleshooting

- **Fetch errors**: Quote the URL in the bash command; ensure `scripts/fetch-stitch.sh` is executable.
- **Component mapping**: Follow [references/contract.md](references/contract.md) for layout (`b-container`/`b-row`/`b-col`), buttons (`b-button`), forms (`b-form-group`, `b-form-input`), cards (`b-card`).

## Keywords

**English:** Stitch, Vue 3, Bootstrap, BootstrapVue, Vite, b-container, b-button.  
**中文关键词：** Stitch、Vue 3、Bootstrap、组件。

## References

- [Contract (Bootstrap mapping)](references/contract.md)
- [Component API (props/events quick reference)](api/component-api.md)
- [Official documentation](references/official.md)
- [Architecture checklist](resources/architecture-checklist.md)
- [Component template](resources/component-template.vue)
- [Stitch API / MCP](https://stitch.withgoogle.com/docs/mcp/guide/)
