---
name: orphan-notes
description: >-
  Use when the user wants an orphan-note sweep in Obsidian (孤儿笔记): find notes
  with no wikilinks to remind them to consider deleting, and surface likely
  related pairs to nudge attention/linking. Read-only by default; never delete
  or mass-link without explicit ask.
---
# 孤儿笔记 (orphan notes)

Proactively (or on ask) scan the Obsidian vault for **orphan notes** and **almost-related** notes. Remind the owner; do not silently clean the library.

## Definitions

- **Orphan (strict)**: a `.md` note with **no outbound `[[wikilink]]`** and **no inbound backlink** from other vault notes (ignore its own title). Embeds `![[…]]` count as links.
- **Weak orphan**: has tags or folder context but still zero wikilinks either way—still report, label as weak.
- **Almost-related**: two or more notes that share strong topical overlap (title/keywords/properties) but do **not** yet link to each other.

Exclude by default (unless they ask to include):

- templates, daily-note shells, MOC index stubs you are told to keep
- `AI outputs/` drafts unless they ask
- attachments-only folders, `.base` / `.canvas` (mention separately only if useful)
- mood / privacy paths named in memory

## When to run

- User says 「孤儿笔记」 / orphan sweep / clean unlinked notes.
- Periodic health check they requested (routine or manual).
- After a large import, offer one sweep.

## Privacy & gates

- Skip emotion / anxiety / voice-diary notes entirely.
- **Never delete** under this skill. Only suggest. Deletion needs an explicit yes per note (or a clear multi-select they confirm).
- **Never mass-add wikilinks** without ask. Suggest pairs; wait.
- Load `obsidian-apprentice-rules` before any write they approve.

## Steps

1. **Resolve vault** — path + machine from memory; confirm reachability.
2. **Build link graph (read-only)** — scan `.md` under the vault (respect exclude list):
   - collect outbound `[[…]]` and `![[…]]` targets (normalize to note ids)
   - invert to backlinks
3. **List orphans** — notes with zero out + zero in. Cap the report at **15**, prioritize:
   - older mtime / clearly abandoned titles first
   - very short empty-ish bodies
   - outside protected folders
4. **List almost-related** — up to **10** pairs/clusters with a one-line why (shared keywords, same project tag, near-duplicate titles). Prefer actionable pairs over huge clumps.
5. **Reply** in two blocks:

### 可能的孤儿（考虑删除或补链）

- [Title](obsidian://…) — 无双链；短注：…（空 / 过时 / 重复嫌疑）

### 可能有关联（提醒关注）

- A ↔ B — 理由：…

Then one ask: delete candidates (list numbers), add suggested links, or ignore. **Wait.**

6. **If they approve deletes** — delete only the named files; confirm paths first; no trash-emptying outside vault tools they use.
7. **If they approve links** — add minimal `[[wikilinks]]` (or a short "See also" line) only on the notes they named; spot-check render; report `obsidian://` links.

## Empty / healthy vault

If few or no orphans: say the graph looks healthy in one sentence; still offer almost-related if any. Do not invent problems.

## Anti-patterns

- Do not shame volume of notes.
- Do not auto-delete "short" notes—short permanent notes are valid.
- Do not turn this into a full re-org or new folder taxonomy.
