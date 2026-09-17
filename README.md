# Sony a6600 Camera Assistant — Claude Skill

A [Claude Skill](https://www.anthropic.com/news/skills) that turns Claude into a working reference for shooting with a Sony a6600: lens-specific shooting advice, a personal lens collection, and reusable settings profiles for common scenarios — all tuned to the a6600's APS-C sensor, IBIS, and menu system rather than generic photography advice.

## What it does

1. **Lens shooting advice** — ask about any lens (owned or hypothetical) and get crop-adjusted focal length, aperture guidance, IBIS/OSS interplay, and AF notes specific to the a6600, informed by a lens-category reference (primes, standard zooms, telephoto/wildlife, macro, wide/astro, video).
2. **Lens collection tracking** — mention a lens you own and Claude tracks it (via its memory feature, so it persists across conversations and devices — see [Notes](#notes) below).
3. **Settings profiles** — baseline, concrete settings (mode, aperture, shutter, ISO, AF, drive) for common scenarios like portrait, action/wildlife, low-light/astro, video, and street — adjustable to the specific lens and conditions you describe, and saveable as named profiles for reuse.

## Installation

### claude.ai / Claude app (web, desktop, mobile)

1. Download `sony-a6600-assistant.skill` from the [latest release](https://github.com/jerdog/sony-a6600-assistant/releases/latest). A `.zip` of the identical archive is attached to the same release, for upload dialogs that only accept `.zip`.
2. Open **Settings → Capabilities** and make sure **"Code execution and file creation"** is turned on. Skills require this; if the Skills section is greyed out, this is why.
3. Go to **Settings → Customize → Skills**.
4. Tap/click **Add custom skill** and upload `sony-a6600-assistant.skill`. If the upload dialog only accepts `.zip`, grab the `.zip` asset from the same release instead — it's the same archive under a different extension.
5. Toggle the skill on.

Skills are tied to your Claude account, not a specific device, so once installed it's available the same way across web, desktop, and mobile without reinstalling anywhere else.

### Claude Code and other CLI-based agents (via `npx`)

If you're using Claude Code, Codex, Cursor, or another agent that supports the open Agent Skills format, you can install straight from this repo using the community [`skills` CLI](https://github.com/Harries/skills-cli) instead of the manual steps above:

```bash
# Install to Claude Code
npx skills add jerdog/sony-a6600-assistant --agent claude-code

# Install to a different agent (see the CLI's docs for supported agents)
npx skills add jerdog/sony-a6600-assistant --agent codex

# List what's in the repo without installing
npx skills add jerdog/sony-a6600-assistant --list
```

This is a third-party CLI, not an official Anthropic tool — check its repo for the current list of supported agents before relying on it. It writes `SKILL.md`/`references/` into whatever skills directory your chosen agent expects, so no manual copying is needed.

## Usage

Once installed, just talk to Claude naturally — you don't need to invoke the skill by name. It triggers automatically when you:

- Mention a Sony lens or ask what settings to use for a shoot
- Reference "the a6600" or "my camera"
- Ask to add or look up a lens in your collection
- Ask what to bring for a specific shoot or trip
- Ask for a settings profile for a scenario (e.g. "what settings for low light with my 15mm")

Example prompts:

```
I just got a Sigma 18-50mm f/2.8. Add it to my lens collection.

What settings should I use for wildlife photography with my 70-350mm?

I'm shooting a wedding indoors — what lens should I bring and what settings profile fits?

Save that as a named profile.
```

## Using with other agents

`SKILL.md` follows the Agent Skills format, which a growing number of tools beyond Claude now read directly (Claude Code, Codex, Cursor, Windsurf, and others — see the `npx skills` install option above). For agents that don't support that format, or for general repo-level context, this repo also includes an **`AGENTS.md`** at the root — a tool-agnostic summary of the same domain knowledge (a6600 body specs, lens shooting guidance, settings profiles) written as plain instructions rather than Claude-specific skill metadata. Point any coding agent or assistant at `AGENTS.md` (or just paste it into a prompt/context window) to get equivalent guidance without needing skill support at all.

One difference to know about: the **memory-backed lens collection and saved profiles** described above are a claude.ai-specific feature. Other agents won't have that persistence automatically — `AGENTS.md` notes a simple file-based fallback (a local `lens-collection.md` you maintain yourself) for tools without an equivalent memory system.

## Notes

- **Lens collection and custom profiles use Claude's memory feature**, not this skill's bundled files — those bundled files (`SKILL.md`, `references/`) are typically read-only once a skill is installed, so personal data that needs to persist and update is stored in Claude's memory instead. This means your lens list and any profiles you save will carry across every conversation and device tied to your account, even though this skill's own files never change.
- This skill encodes general Sony a6600 body specs and settings guidance based on publicly available specifications — always sanity-check against your own copy of the manual, especially if firmware updates change behavior.
- Not affiliated with or endorsed by Sony.

## Repo contents

```
sony-a6600-assistant/                 # repo root — this IS the skill
├── SKILL.md                          # Skill definition (Claude Skills format); metadata.version holds the version
├── AGENTS.md                         # Tool-agnostic version for other agents
├── CLAUDE.md                         # Maintainer notes: versioning + release process
├── README.md                         # This file
├── LICENSE                           # MIT
├── references/
│   ├── lens-shooting-guide.md        # Advice by lens category
│   └── settings-profiles.md          # Baseline scene/lens profiles
└── .github/workflows/
    └── release.yml                   # Builds and publishes the archive on `v*` tags
```

## Versioning and releases

The skill's version lives in `metadata.version` in `SKILL.md`'s frontmatter (a bare top-level `version:` key isn't part of the accepted schema and will fail validation), and git tags mirror it as `v<version>`. Pushing a `v*` tag triggers the release workflow, which verifies the tag matches the declared version (failing loudly if they've drifted), builds the archive, and publishes it to the Releases page as both `.skill` and `.zip`.

The published archive contains only `SKILL.md` and `references/`, nested under a `sony-a6600-assistant/` folder — the repo's own docs aren't part of what gets installed. A `.skill` file is just a zip archive with a different extension, so you can also build one by hand from those two paths.

### Cutting a new release

Only a `v*` tag triggers a build. Pushing to `main` on its own publishes nothing, and the tag must match `metadata.version` exactly or the workflow fails before anything reaches the Releases page.

Pick the bump level first:

- **patch** — typo, wording, or formatting fix; nothing about what the skill tells an agent to do has changed
- **minor** — new guidance, a new reference file, expanded coverage
- **major** — restructured skill, renamed or removed reference files, changed trigger conditions

Then, using `1.1.0` as the example:

```bash
# 1. set metadata.version in SKILL.md to 1.1.0

# 2. commit the skill edits and the version bump together
git add SKILL.md AGENTS.md
git commit -m "Add filter inventory tracking"

# 3. tag it to match, then push commit and tag together
git tag -a v1.1.0 -m "v1.1.0 — filter inventory tracking"
git push --follow-tags

# 4. watch the build
gh run watch
```

Use an **annotated** tag (`git tag -a`). `git push --follow-tags` skips lightweight tags, so a plain `git tag v1.1.0` pushes the commit, pushes no tag, and triggers nothing — which looks identical to a broken workflow.

For commit messages, let the subject say what changed and the body say why the previous behavior was inadequate; the diff already covers the what.

If the tag and the declared version disagree, the build stops with `Tag v1.1.0 implies version 1.1.0, but SKILL.md declares 1.0.1` and publishes nothing. Fix the version, commit, then move the tag:

```bash
git tag -d v1.1.0 && git push origin :refs/tags/v1.1.0   # drop the bad tag
git tag -a v1.1.0 -m "v1.1.0 — ..." && git push --follow-tags
```

Docs-only changes (`README.md`, `AGENTS.md`, `CLAUDE.md`, `LICENSE`) don't need a version bump — they aren't part of the published archive.

## License

MIT — do whatever you'd like with it.
