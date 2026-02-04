# Alignment with Official Google Stitch Skills

This repository **subsumes and strengthens** [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills). Every official skill has a **local equivalent that is better or equal** in capability and is integrated with this repo’s MCP wrappers and framework specs.

## Official → Local Mapping (Local Stronger)

| Official | Local (this repo) | Why local is stronger |
|----------|-------------------|------------------------|
| **design-md** | **stitch-design-md** | **Stronger:** DESIGN.md includes **Section 6** (Design System Notes for Stitch Generation) for copy-paste into prompts; official has only sections 1–5. Explicit stitch-mcp-* names (format: stitch-mcp-<tool>, e.g. get_screen → stitch-mcp-get-screen); integrates with stitch-ui-prompt-architect and stitch-loop; references framework design specs. |
| **enhance-prompt** | **stitch-ui-prompt-architect** | **Stronger:** Two paths: (1) Vague → enhanced prompt (same as official); (2) Design Spec + Request → sectioned Stitch prompt. Plus framework contract prefix (uView, Element, Layui, Bootstrap, Vant), KEYWORDS.md, and next-prompt.md for stitch-loop. |
| **stitch-loop** | **stitch-loop** | **Stronger:** Same baton/SITE.md; **Step 4.5** optional Visual Verification with Chrome DevTools MCP; **Orchestration Options** (CI/CD, human-in-loop, agent chains, manual); explicit stitch-mcp-* names; DESIGN.md Section 6; prompt quality via stitch-ui-prompt-architect. |
| **react-components** | **stitch-react-components** | Same retrieval + fetch script + architecture checklist + component template; references stitch-mcp-* for project/screen discovery; optional DESIGN.md alignment (stitch-design-md). |
| **remotion** | **stitch-remotion** | **Stronger:** Same walkthrough workflow; **Common patterns** (slide show, feature highlight, user flow); **Voiceover** and **dynamic text extraction**; **Remotion Skills** and **Remotion MCP** links; stitch-mcp-* names; DESIGN.md for overlay text. |
| **shadcn-ui** | **stitch-shadcn-ui** | **Stronger:** Same discovery, install, customize, blocks; **init styles** (Vega, Nova, Maia, Lyra, Mira); **custom registries** (get_project_registries, list_items_in_registries); **Validation and Quality** checklist; integrates with stitch-react-components and DESIGN.md. |

## What This Repo Adds Beyond Official

- **stitch-mcp-***: One skill per MCP tool (create_project, list_projects, get_project, generate_screen_from_text, list_screens, get_screen). Skill name = MCP tool name with underscores → hyphens (e.g. generate_screen_from_text → stitch-mcp-generate-screen-from-text). Full mapping: [mcp-naming-convention.md](mcp-naming-convention.md).
- **stitch-ui-design-spec-***: Framework-specific design contracts (Layui, Ant Design, Bootstrap, Element Plus, uView, uView Pro, Vant) for Stitch prompts.
- **stitch-ui-designer**: Master orchestrator for end-to-end design tasks.
- **stitch-ui-design-spec-generator**: Structured spec (theme, device, style) from vague requests.
- **stitch-skill-creator**: Factory for new scenario skills.
- **stitch-ued-guide**: UED guidelines and visual vocabulary.
- **Stitch → Framework Components**: Six conversion skills (parallel to stitch-react-components) that turn Stitch screens into runnable projects:
  - **stitch-vue-element-components**, **stitch-vue-bootstrap-components**, **stitch-vue-layui-components**, **stitch-vue-vant-components** (Vite + Vue 3 + component library).
  - **stitch-uview-components**, **stitch-uviewpro-components** (uni-app + uView 2 / uView Pro).
- **agents/stitch-ui-designer.md**: Dedicated agent for Stitch UI workflows.

## When to Use Which

- **All Stitch flows**: Prefer this repo’s skills (stitch-*). They reference each other and the same MCP; local prompt-architect is strictly stronger than official enhance-prompt (dual path + framework contracts).
- **Reference only**: Use official [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills) for additional examples or scripts (e.g. react-components validate.js, remotion templates) if you need them; local skills document or link to the same patterns.

All Stitch docs (prompting, device types, MCP) apply to both: [Stitch Learn](https://stitch.withgoogle.com/docs/learn/overview/), [MCP Guide](https://stitch.withgoogle.com/docs/mcp/guide/).

## Keeping local ahead of official

When syncing with [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills):

1. **Compare SKILL.md** for each official skill (design-md, enhance-prompt, react-components, stitch-loop, remotion, shadcn-ui) and ensure the local equivalent keeps or adds every official feature, plus local-only additions (MCP skill names, framework contracts, Section 6, etc.).
2. **MCP naming**: Local skills use **stitch-mcp-<tool>** from the MCP tool name (e.g. get_screen → stitch-mcp-get-screen; do not use stitch-mcp-get-screen (old style)). Full table: [mcp-naming-convention.md](mcp-naming-convention.md).
3. **New official skills**: If official adds a new skill, add a local equivalent under `skills/` and document it in this table and in README.

For design-spec vs conversion skill roles (inputs, outputs, when to use which), see [skills-compare-design-spec-and-react.md](skills-compare-design-spec-and-react.md) (English) or [skills-compare-design-spec-and-react.zh-CN.md](skills-compare-design-spec-and-react.zh-CN.md) (中文).
