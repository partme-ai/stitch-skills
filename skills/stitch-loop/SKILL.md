---
name: stitch-loop
description: Iteratively build multi-page websites using Stitch with a baton-passing loop. Reads next-prompt.md, generates pages via Stitch MCP (create_project, generate_screen_from_text, get_screen), integrates into site, updates SITE.md and next-prompt.md. Use with stitch-design-md and stitch-ui-prompt-architect for design consistency.
allowed-tools:
  - "stitch*:*"
  - "chrome*:*"
  - "Read"
  - "Write"
  - "Bash"
---

# Stitch Build Loop

**Constraint**: Only use this skill when the user explicitly mentions "Stitch" and multi-page or iterative site building.

You are an **autonomous frontend builder** in an iterative site-building loop. Each iteration: (1) Read the baton (`next-prompt.md`), (2) Generate a page with Stitch MCP, (3) Integrate into the site, (4) Write the next baton so the loop continues.

## Prerequisites

**Required:**
- Stitch MCP Server (see https://stitch.withgoogle.com/docs/mcp/guide/)
- A Stitch project (create with `stitch-mcp-create-project` or MCP `create_project` if needed)
- `DESIGN.md` (generate with **stitch-design-md** from an existing screen if missing)
- `SITE.md` (site vision, Stitch Project ID, sitemap, roadmap)

**Optional:** Chrome DevTools MCP for visual verification of generated pages.

## The Baton System

`next-prompt.md` is the relay baton between iterations:

```markdown
---
page: about
---
A page describing how jules.top tracking works.

**DESIGN SYSTEM (REQUIRED):**
[Copy from DESIGN.md Section 6]

**Page Structure:**
1. Header with navigation
2. Explanation of tracking methodology
3. Footer with links
```

**Rules:**
- The `page` frontmatter field determines the output filename (e.g. `about.html`).
- Prompt body must include the design system block from `DESIGN.md`.
- You **MUST** update `next-prompt.md` before completing so the loop continues.

## Execution Protocol

### Step 1: Read the Baton

Parse `next-prompt.md`: extract `page` from frontmatter and the full prompt from the body.

### Step 2: Consult Context Files

| File | Purpose |
|------|--------|
| `SITE.md` | Site vision, **Stitch Project ID**, sitemap (Section 4), roadmap (Section 5), creative freedom (Section 6) |
| `DESIGN.md` | Visual style; copy Section 6 into each baton prompt |

**Checks:** Do not recreate pages already in Section 4 (Sitemap). Pick next task from Section 5 (Roadmap) or Section 6 (Creative Freedom) if roadmap is empty.

### Step 3: Generate with Stitch

Use Stitch MCP (or skills **stitch-mcp-create-project**, **stitch-mcp-generate-screen-from-text**, **stitch-mcp-get-screen**):

1. **Discover prefix**: Run `list_tools` to find the Stitch MCP prefix.
2. **Get or create project**: If `stitch.json` exists, use its `projectId`; else call `[prefix]:create_project` and save ID to `stitch.json`.
3. **Generate screen**: Call `[prefix]:generate_screen_from_text` with `projectId`, `prompt` (full baton content including DESIGN SYSTEM), `deviceType` (e.g. DESKTOP).
4. **Retrieve assets**: Call `[prefix]:get_screen`; download `htmlCode.downloadUrl` → `queue/{page}.html`, `screenshot.downloadUrl` → `queue/{page}.png`.

### Step 4: Integrate into Site

1. Move `queue/{page}.html` → `site/public/{page}.html`.
2. Fix asset paths to be relative to the public folder.
3. Update navigation: wire placeholder links (`href="#"`) to the new page; add to global nav if appropriate.
4. Keep headers/footers consistent across pages.

### Step 4.5: Visual Verification (Optional)

If **Chrome DevTools MCP** is available, verify the generated page:

1. Run `list_tools` to see if `chrome*` tools are present.
2. Start a local server (e.g. `npx serve site/public`).
3. Use `[chrome_prefix]:navigate` to open `http://localhost:3000/{page}.html`.
4. Use `[chrome_prefix]:screenshot` to capture the rendered page.
5. Compare with the Stitch screenshot (`queue/{page}.png`) for fidelity.
6. Stop the server when done.

If Chrome DevTools MCP is not installed, skip to Step 5.

### Step 5: Update Site Documentation

Update `SITE.md`: add the new page to Section 4 (Sitemap) with `[x]`; remove consumed ideas from Section 6; update Section 5 if a backlog item was completed.

### Step 6: Prepare the Next Baton (Critical)

**You MUST update `next-prompt.md` before completing.**

1. Choose next page: Section 5 (Roadmap) → Section 6 (Creative Freedom) → or invent one that fits the vision.
2. Write `next-prompt.md` with valid YAML frontmatter (`page: <name>`) and full prompt body including **DESIGN SYSTEM (REQUIRED)** copied from DESIGN.md.

## File Structure

```
project/
├── next-prompt.md      # Baton — current task
├── stitch.json         # Stitch project ID (persist!)
├── DESIGN.md           # From stitch-design-md
├── SITE.md             # Vision, sitemap, roadmap
├── queue/              # Staging: {page}.html, {page}.png
└── site/public/        # Production: index.html, {page}.html
```

## Orchestration Options

The loop can be driven by different triggers (local exceeds official by documenting all options):

| Method | How it works |
|--------|--------------|
| **CI/CD** | GitHub Actions or similar runs on `next-prompt.md` changes. |
| **Human-in-loop** | Developer reviews each iteration before continuing. |
| **Agent chains** | One agent dispatches to another (e.g. Jules API). |
| **Manual** | Developer runs the agent repeatedly with the same repo. |

The skill is orchestration-agnostic; focus on the baton pattern, not the trigger.

## Integration with This Repo

- **DESIGN.md**: Create with **stitch-design-md** from an existing Stitch screen; copy Section 6 into every baton prompt.
- **Prompt quality**: Use **stitch-ui-prompt-architect** to enhance vague baton text or to merge design spec + request into a Stitch-ready prompt.
- **MCP tools**: Use **stitch-mcp-create-project**, **stitch-mcp-generate-screen-from-text**, **stitch-mcp-get-screen** (or underlying MCP) for create/generate/get.

## Common Pitfalls

- ❌ Forgetting to update `next-prompt.md` (loop stops)
- ❌ Recreating a page already in the sitemap
- ❌ Omitting the design system block from the prompt
- ❌ Leaving `href="#"` instead of wiring real links
- ❌ Not persisting `stitch.json` after creating a project

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Stitch generation fails | Ensure prompt includes DESIGN SYSTEM block from DESIGN.md |
| Inconsistent styles | Keep DESIGN.md up to date; copy Section 6 correctly |
| Loop stalls | Verify `next-prompt.md` has valid frontmatter and body |
| Broken navigation | Use correct relative paths for internal links |

## Keywords

**English:** stitch-loop, baton, next-prompt, SITE.md, DESIGN.md, multi-page, iterative.  
**中文关键词：** stitch-loop、接力、next-prompt、多页、迭代建站。

## References

- [Examples](examples/usage.md)
- [SITE.md Template](examples/SITE.md)
- [Next Prompt Template](examples/next-prompt.md)
