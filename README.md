# Sony a6600 Camera Assistant — Claude Skill

A [Claude Skill](https://www.anthropic.com/news/skills) that turns Claude into a working reference for shooting with a Sony a6600: lens-specific shooting advice, a personal lens collection, and reusable settings profiles for common scenarios — all tuned to the a6600's APS-C sensor, IBIS, and menu system rather than generic photography advice.

## What it does

1. **Lens shooting advice** — ask about any lens (owned or hypothetical) and get crop-adjusted focal length, aperture guidance, IBIS/OSS interplay, and AF notes specific to the a6600, informed by a lens-category reference (primes, standard zooms, telephoto/wildlife, macro, wide/astro, video).
2. **Lens collection tracking** — mention a lens you own and Claude tracks it (via its memory feature, so it persists across conversations and devices — see [Notes](#notes) below).
3. **Settings profiles** — baseline, concrete settings (mode, aperture, shutter, ISO, AF, drive) for common scenarios like portrait, action/wildlife, low-light/astro, video, and street — adjustable to the specific lens and conditions you describe, and saveable as named profiles for reuse.

## Installation

### claude.ai / Claude app (web, desktop, mobile)

1. Download `sony-a6600-assistant.skill` from this repo (or clone the repo and zip the `sony-a6600-assistant/` folder yourself — see [Repo contents](#repo-contents)).
2. Open **Settings → Capabilities** and make sure **"Code execution and file creation"** is turned on. Skills require this; if the Skills section is greyed out, this is why.
3. Go to **Settings → Customize → Skills**.
4. Tap/click **Add custom skill** and upload `sony-a6600-assistant.skill`. If the upload dialog only accepts `.zip`, rename the file's extension to `.zip` first — it's the same file either way.
5. Toggle the skill on.

Skills are tied to your Claude account, not a specific device, so once installed it's available the same way across web, desktop, and mobile without reinstalling anywhere else.

### Claude Code and other CLI-based agents (via `npx`)

If you're using Claude Code, Codex, Cursor, or another agent that supports the open Agent Skills format, you can install straight from this repo using the community [`skills` CLI](https://github.com/Harries/skills-cli) instead of the manual steps above:

```bash
# Install to Claude Code
npx skills add <your-github-username>/sony-a6600-assistant --agent claude-code

# Install to a different agent (see the CLI's docs for supported agents)
npx skills add <your-github-username>/sony-a6600-assistant --agent codex

# List what's in the repo without installing
npx skills add <your-github-username>/sony-a6600-assistant --list
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

I'm shooting a wedding indoors — what lens should I bring and what
settings profile fits?

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
sony-a6600-assistant/
├── SKILL.md                          # Skill definition (Claude Skills format)
├── AGENTS.md                         # Tool-agnostic version for other agents
├── references/
│   ├── lens-shooting-guide.md        # Advice by lens category
│   └── settings-profiles.md          # Baseline scene/lens profiles
└── README.md                         # This file
```

To repackage after making changes, use Anthropic's `skill-creator` packaging script, or simply zip the `sony-a6600-assistant/` folder — a `.skill` file is just a zip archive with that extension.

## License

MIT — do whatever you'd like with it.
