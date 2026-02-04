# Contributing to Stitch Skills

Thank you for considering contributing to this repository. The following guidelines help keep skills consistent and discoverable by AI agents.

## Before you start

- Read [README.md](README.md) and [AGENTS.md](AGENTS.md) for repo structure and skill conventions.
- Skills follow the [Agent Skills Specification](https://agentskills.io/specification). Stay aligned with the standard so skills work across Claude Code, Cursor, Trae, and other agents.

## Contribution process

1. **Fork** the repository.
2. **Create a feature branch** (e.g. `skill/your-skill-name` or `docs/improve-readme`).
3. **Implement** your change:
   - New skills: use the [Repository Structure](README.md#repository-structure-agent-skills-standard) (SKILL.md, examples/, optional references/, scripts/, LICENSE.txt).
   - Use **stitch-skill-creator** for new scenario skills when applicable.
   - For MCP wrappers, follow the `stitch-mcp-<tool>` naming and one MCP tool per skill.
4. **Commit** with clear messages (e.g. "Add stitch-ui-xxx skill", "Docs: align README with upstream structure").
5. **Push** to your fork and open a **Pull Request** against the default branch.
6. **Respond** to review feedback; maintainers may ask for edits before merge.

## Skill checklist (new or updated skills)

- [ ] `SKILL.md` has YAML frontmatter with `name` and `description`.
- [ ] `name` matches the skill directory name (kebab-case).
- [ ] `examples/` contains at least one usage example (e.g. `usage.md` or a gold-standard sample).
- [ ] Optional: `references/` or `scripts/` if the skill needs extra docs or automation.
- [ ] Optional: `allowed-tools` in frontmatter if the skill should restrict which tools the agent uses.
- [ ] Trigger safety: execution/orchestration skills only activate when the user explicitly mentions "Stitch" (or as documented).
- [ ] LICENSE.txt present if the skill is distributed with a license.

## Code of conduct

Be respectful and constructive in issues and pull requests. This project is not part of an official Google product; it follows the same spirit of openness as [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills).

## Questions

Open an issue for questions about structure, naming, or how your skill fits into the existing set (MCP, design spec, orchestrator, etc.).
