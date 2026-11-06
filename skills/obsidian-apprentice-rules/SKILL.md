---
name: obsidian-apprentice-rules
description: >-
  Use whenever importing, organizing, or writing into the owner's Obsidian
  vault; enforces Kepano-aligned apprentice constraints.
---
# Obsidian Apprentice rules

Apply on every vault task. Source mindset: [Kepano · How I use Obsidian](https://stephango.com/vault).

## Hard rules
1. **File over app** — real `.md` only; standard Markdown; no invented syntax.
2. **Sparse folders** — new notes default to vault root unless the owner says otherwise; `Clippings/` for other people's writing; your authored output only under `AI outputs/` (or their named AI-output folder); no silent mass re-filing.
3. **Wikilinks first** — keep and complete `[[wikilinks]]`; never peel concepts into bare words without brackets.
4. **Unresolved links OK** — leave `[[Name]]` as breadcrumbs; do not batch-create empty stub notes for missing targets.
5. **Clipping quality gate** — import only usable full text. Before writing: spot-check ≥1 note for long body, presence of `[[ ]]`, and that concept notes can grow backlinks. Reject "summary + full text on X" shells.
6. **Don't understand for them** — you may scan, clean, and file; elevating ideas into claims and random revisits stay with the owner.
7. **Minimal properties** — add YAML only when needed; don't invent experimental fields.
8. **Ask first** — major deletes and batch moves need the owner's go-ahead.
9. **Lived-experience gate for publishable drafts** — when turning notes into outward writing, keep only what the owner actually did; don't invent experience.

## Import checklist
- [ ] Spot-check ≥1 note: full body, not a redirect shell
- [ ] Concepts appear as `[[Concept]]`, not plain tokens
- [ ] Concept notes link back with `[[Article title]]` (or backlinks will appear after save)
- [ ] Destination folder matches map (others → Clippings; your output → AI outputs)
- [ ] No mass empty stubs for missing links

## Anti-pattern
Importing open-source summary shells and converting Concepts' `[[links]]` to plain text — backlink graph goes to zero. Never repeat.
