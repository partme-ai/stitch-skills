# stitch-vue-layui-components Usage

## When to use

- User has a Stitch screen and wants **Vue 3 + Layui-Vue** (Vite, .vue SFC) components that match the design.
- You need to download Stitch HTML reliably (use `scripts/fetch-stitch.sh` when web_fetch fails on GCS URLs).

## Steps

1. Get projectId and screenId (e.g. via stitch-mcp-project-list, stitch-mcp-screen-list).
2. Call Stitch MCP get_screen; get `htmlCode.downloadUrl`.
3. Run `bash scripts/fetch-stitch.sh "<url>" temp/source.html`.
4. Parse HTML; map to Layui-Vue components per references/contract.md; create Vue SFCs using resources/component-template.vue and src/data/mockData.js.
5. Wire components in App.vue or router; verify against resources/architecture-checklist.md; run `npm run dev`.

## Example user prompt

> "Convert the Stitch admin screen to a Vue 3 + Layui project."
