# Jackywine Digital Garden Skills

Agent skills for a **dual-layer digital garden**: **flomo as L1 memory** (flash notes, tweet ingest) and **local Obsidian as disk** (full-text clippings, dense `[[wikilinks]]`).

These follow the [Agent Skills specification](https://agentskills.io/specification) so they work with skills-compatible agents (Grok Bot, Claude Code, Codex, OpenCode, etc.).

> Companion toolkit: install [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) for Obsidian Flavored Markdown, Bases, JSON Canvas, CLI, Defuddle, and Knap. This repo does **not** vendor those six skills.

## What you get

| Skill | Id | Role |
|-------|-----|------|
| Digital garden onboarding | `digital-garden-onboarding` | Install-time setup, one question at a time |
| Getting started | `getting-started-2` | First-chat walkthrough (flomo + vault) |
| flomo tweet ingest | `flomo` | Plain-text intro + bare X URL; optional `#Grokbot/Import` tag |
| Obsidian clipping | `obsidian` | Full-text clip + wikilinks + quality gate |
| Apprentice rules | `obsidian-apprentice-rules` | Kepano-aligned vault write constraints |
| Related notes | `related-notes` | After today’s idea → search library, give reasons + links |
| Orphan notes | `orphan-notes` | Find unlinkable orphans + almost-related pairs (read-only by default) |

## Install

### npx skills

```sh
npx skills add https://github.com/Jackywine/jackywine-digital-garden-skills
```

(Replace the GitHub path with the real repo URL after first publish.)

Also add Kepano’s pack:

```sh
npx skills add https://github.com/kepano/obsidian-skills
```

### Manual

Copy each folder under `skills/` into your agent’s skills directory (one `SKILL.md` per skill). Keep relative `references/` folders intact when present.

### Grok Bot

Import or paste skills into your shared skill library, then point a specialty bot (Digital Garden) at them. Run `digital-garden-onboarding` on first chat.

## Design principles

- **Dual-layer** — flash / tweet ammo → flomo; long clippings & concept nets → Obsidian
- **File over app** — real `.md`, sparse folders, wikilinks first
- **Curate, don’t regurgitate** — related notes need a one-line *why*; never restate what the owner just wrote
- **Privacy** — skip mood / anxiety / voice-diary memos in reports
- **Ask first** — no mass delete, mass link, publish, or deploy without an explicit yes
- **Lived-experience gate** — outward drafts only keep what the owner actually did

## Suggested bot persona (short)

> Dual-layer digital garden. flomo as L1; local Obsidian as disk. Tweet ingest with bare links; full-text clippings; related-notes + orphan-notes sweeps; install-time onboarding. Does not publish, deploy, or invent lived experience.

## License

MIT © Jackywine

Kepano skills remain under their own license — use them from upstream, do not copy into this repo.
