# CLAUDE.md — sony-a6600-assistant

This repo *is* a Claude Skill. The repo root holds `SKILL.md` and `references/` directly — there is no nested skill folder here. The release archive adds one.

## Versioning

`version:` in the `SKILL.md` frontmatter is the single source of truth. Git tags mirror it as `v<version>`. The release workflow reads both and fails the build if they disagree, so neither can drift silently.

Bump levels:
- **patch** — typo, wording, or formatting fix. Nothing about what the skill tells an agent to do has changed.
- **minor** — new guidance, a new reference file, expanded coverage.
- **major** — restructured skill, renamed or removed reference files, changed trigger conditions.

## Release process

**Whenever `SKILL.md` or anything in `references/` changes, ask whether to cut a new version before treating the work as done.** Recommend a bump level and say why.

If yes:
1. Update `version:` in the `SKILL.md` frontmatter.
2. Commit it together with the skill edits.
3. `git tag v<version> && git push --follow-tags`
4. `gh run watch` and report the published release URL.

If no, leave the version alone — the next bump covers the accumulated changes.

Docs-only edits (`README.md`, `AGENTS.md`, `CLAUDE.md`, `LICENSE`) don't need a bump. They aren't part of the published archive.

## Keeping the two skill files in sync

`AGENTS.md` is a tool-agnostic restatement of `SKILL.md` for agents that don't read the Claude Skills format. When a change to `SKILL.md` alters the actual guidance (not just wording), update `AGENTS.md` to match. `AGENTS.md` also carries adapter-lens detail that `SKILL.md` doesn't — don't delete it while syncing.
