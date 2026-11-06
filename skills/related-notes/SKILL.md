---
name: related-notes
description: >-
  Use when the user shares today's idea, thought, or note and wants related
  notes from the vault (相关笔记); or asks what in the library connects to what they
  just said. Search flomo (if connected) and Obsidian for related notes with
  reasons and links—do not only restate what they wrote.
---
# 相关笔记 (related notes)

When the owner shares a fresh idea, thought, or note (today or "just now"), surface **related notes already in the library**—not a rewrite of what they said.

## When to run

- They dump a thought and ask what connects, or say 「相关笔记」 / related notes.
- A morning or evening prompt: remind them to share today's idea; after they answer, run this skill.
- Do **not** invent relatedness. If nothing solid, say so in one line.

## Privacy & gates

- Skip mood / anxiety / voice-diary privacy memos: never search, cite, or link them.
- Lived-experience gate: do not pad with made-up personal history.
- Prefer read-only search. Do not add `[[wikilinks]]` or rewrite their notes unless they explicitly ask to link.

## Inputs

1. Their plain-language idea (required).
2. Optional: date window, folder, or tag to narrow.
3. Vault path + machine from memory / onboarding; flomo via official MCP when available.

## Steps

1. **Normalize the seed** — extract 3–8 keywords / entities / themes (topics, tools, people, projects). Drop filler.
2. **Search Obsidian (disk)** — use vault search / CLI / file search on the owner's machine:
   - title + body match on keywords
   - existing `[[wikilinks]]` and backlinks around hits
   - tags / properties if present
   - Prefer notes they wrote over pure `Clippings/` unless the clip is clearly on-topic.
3. **Search flomo (L1)** when connected — same themes; skip privacy-tagged / mood notes.
4. **Rank** — pick at most **5** strong hits (fewer is fine). Score by: shared concepts, reciprocal links, recency only as a tie-break.
5. **Reply** — short lead line, then one bullet per hit:
   - note title as clickable `obsidian://open?vault=VAULT_NAME&file=relative/path` (spaces `%20`), or flomo note link if that is the source
   - **one sentence why** it relates (specific overlap, not "also about notes")
   - optional: 1–2 existing `[[wikilink]]` neighbors if they strengthen the cluster
6. **Offer next step** (one line, wait): add a wikilink between seed and hit; clip today's idea into flomo with `#Grokbot/Import`; or deepen one hit. Do nothing until they pick.

## Output shape

```
和「…」可能相关的笔记：

- [Title](obsidian://…) — 理由：…
- …

要我帮你加双链 / 写进 flomo / 展开其中一条吗？
```

If zero hits: 「库里没找到靠谱相关笔记；要不要把这条先记进 flomo？」

## Anti-patterns

- Do not dump a long unread list.
- Do not restate their whole note as the "related" item.
- Do not batch-edit the vault under this skill.
