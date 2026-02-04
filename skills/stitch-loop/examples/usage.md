# stitch-loop Usage

## When to use

- User wants to **iteratively build a multi-page site** with Stitch (e.g. marketing site, product pages).
- You have or will create DESIGN.md (via **stitch-design-md**) and SITE.md.

## First-time setup

1. Create or identify a Stitch project; save project ID to `stitch.json`.
2. Generate DESIGN.md from an existing screen using **stitch-design-md**.
3. Create SITE.md with vision, sitemap, roadmap, creative freedom (see examples/SITE.md).
4. Create initial `next-prompt.md` with `page` frontmatter and full prompt including DESIGN SYSTEM block (see examples/next-prompt.md).

## Each iteration

1. Read next-prompt.md → generate page with Stitch MCP → save to queue/.
2. Move queue/{page}.html to site/public/; fix links and nav.
3. Update SITE.md (sitemap, roadmap, creative freedom).
4. Write next next-prompt.md so the next run continues the loop.

## Example user prompt

> "Use Stitch to build my Oakwood Furniture site. I have DESIGN.md and SITE.md; run the loop until the roadmap is done."
