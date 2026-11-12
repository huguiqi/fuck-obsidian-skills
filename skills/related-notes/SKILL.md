---
name: related-notes
display_name: 关联笔记
display_name_en: Related Notes
description_zh: 分享一个想法 → 在 raw/wiki 找 ≤5 条相关笔记，一条一句“为什么” + 路径。
description_en: Share a thought and find up to 5 related notes in raw/wiki, each with a one-line reason and file path.
version: "1.0.0"
author: xiaohei_spring
description: Use when the user shares a thought/idea, or wants to find notes related to one, in the raw/wiki knowledge base. Find up to 5 related notes with one-line reasons and file paths; never echo the user's own words back.
---

# related-notes — 找相关笔记

> 方法论角色：关联索引的检索面。在 `raw/`、`wiki/` 里找和当下想法真正相关的条目，给可点的路径和一句"为什么"。

## 0 · 一条底线
**永远不把用户刚说的话复述回去。** 结果只做一件事：把他自己的思考**连接到他知识库里已有的知识**。

## 1 · 输入
- 用户分享想法 / 问"有什么相关的笔记 / 来源 / 概念" / 点开某条 `[[C-###]]`、`[[S-###]]`。
- 输入可以是自由的想法、问题、一段链接，或某个条目名。

## 2 · 找什么
在 `raw/`、`wiki/`（含 `summaries`、`concepts`、`indexes`）里找真正相关的条目：
**同主题 / 提供证据 / 提供反例 / 提供概念框架 / 提供背景**的，都算相关。

**不相关就明说**——不为凑数塞弱相关的条目。

## 3 · 怎么找
1. **直接命中**：标题、`[[双链]]`、概念名、frontmatter `tags`、`source`。
2. **上下文召回**：读摘要/概念的定义、正文里的应用，找语义相关的条目（LLM 读懂，不只关键词）。
3. **来源回溯**：从概念 → 来源 `[[S-###]]` → 该来源下的其它概念。

## 4 · 输出格式
```
想："[用户的想法]"
---
[条目名/概念名] — 为什么相关（一句话）
  路径：wiki/concepts/C-### xxx.md
[条目名/概念名] — 为什么相关（一句话）
  路径：raw/articles/S-### xxx.md
```
- 原则：**一条笔记一句"为什么"** + 一个**文件路径**（相对 `raw/`、`wiki/` 的路径或 `[[wikilink]]`，不报 `obsidian://`）。
- **≤5 条**，按相关度排。

## 5 · 边界
- 只在 `raw/`、`wiki/` 里找，不越界到 `outputs/`、平台成品目录。
- **只读**：不新建、不改、不删笔记。建议写进"相关"区由用户定。
- 没有相关就说**没找到**，别硬凑。
