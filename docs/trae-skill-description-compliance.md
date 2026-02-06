# Trae / Simple-Parser Skill Description Compliance

## Problem

Some tools that discover skills from `.trae/skills` (or other agent skill dirs) do **not** parse YAML frontmatter. They use a "simple" rule: take the **first non-empty, non-`#` line** of `SKILL.md` as the skill description. Stitch skills had frontmatter like:

```yaml
---
name: stitch-mcp-get-screen
description: Get screen details from Stitch (htmlCode, screenshot, dimensions)...
---
```

Immediately after the closing `---`, the next non-empty line was often a blank line, then `# Title`, then `**Constraint**...`. So the simple parser would get:

- Either nothing useful (blank),
- Or a frontmatter line such as `name: stitch-mcp-get-screen`,
- Or `**Constraint**: ...`

So the **description** shown in Trae (or partme list, or any UI that uses "first line" as description) was wrong or unhelpful.

## Solution

1. **Spec** ([spec/agent-skills-spec.md](../spec/agent-skills-spec.md)): Require that the **first non-empty line after the closing `---`** be a single-line short description (same as or a concise version of frontmatter `description`).

2. **All stitch-skills SKILL.md**: A one-line description was added right after the closing `---`, before the main `# Title`. Example:

   ```markdown
   ---
   name: stitch-mcp-get-screen
   description: Get screen details from Stitch (htmlCode, screenshot, dimensions)...
   ---

   Get screen details from Stitch. Returns htmlCode.downloadUrl, screenshot, width, height, title.

   # Stitch MCP Get Screen (stitch-mcp-get-screen)
   ```

3. **Parsers**:
   - **YAML/frontmatter** (e.g. partme-cli-ts `skills add`, full-stack-skills `convert_to_trae.py`): Continue to use `name` and `description` from frontmatter.
   - **Simple "first non-# line"**: Now get the new first line as the description.

## Verification

- Run Trae converter: `python3 full-stack-skills/adapters/trae/convert_to_trae.py --all stitch-skills/skills /tmp/out` — all 30 skills should convert successfully; `trae-plugin.json` still uses frontmatter.
- If your tool lists skills by scanning `.trae/skills/*/SKILL.md` and taking the first non-# line as description, that line is now the intended short description for every stitch skill.

## New Skills

When adding a new skill under `stitch-skills/skills/`, follow the spec: after the closing `---`, add one line with the short description, then the main heading and body.

## Trae-safe description line

Some simple parsers (including Trae) can misparse the description if it contains:

- **Colon `:` in the middle** — e.g. `Tool for X: outputs Y` may be split as key/value; use a period instead: `Tool for X. Outputs Y`.
- **Parentheses `( )` or slash-heavy text** — e.g. `(Vue 3 / Desktop)` can cause issues; prefer `for Stitch` or `for Stitch Vue 3 Desktop` without parentheses/slashes in the first line.
- **Plus `+`** — e.g. `prefix or selector JSON + assembled prompt` → use `and` instead: `prefix or selector JSON and assembled prompt`.

Keep the **first line after `---`** (and the frontmatter `description` if the UI reads it) to a single sentence with only letters, spaces, dots, hyphens, and simple words so Trae and similar tools reliably show the description.
