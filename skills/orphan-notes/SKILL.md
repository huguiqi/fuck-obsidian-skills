---
name: orphan-notes
display_name: 孤岛检查
display_name_en: Orphan Notes
description_zh: 孤儿笔记/健康检查：零双链 + 近关联配对，默认只读。
description_en: Orphaned-notes health check — zero-backlink notes plus near-association pairing, read-only by default.
version: "1.0.0"
author: xiaohei_spring
description: Use when the user asks for an orphaned-notes check / 健康检查 / 孤岛扫描 of the wiki, or wants to see notes with no backlinks and their near-associations. 只读、可解释，绝不擅自删/链/挪。
---

# orphan-notes — 孤岛扫描（健康检查）

> 方法论角色：Karpathy 健康检查的**孤岛**项（另两项：一致性、完整性）。扫零双链条目 + 近关联配对，给理由和路径，**不擅自处置**。

## 0 · 任务（默认是"看"，不是"动"）
1. **找孤儿**：列出**零入链**的 `[[条目]]`（≤15）。
2. **近关联**：每个孤儿找近关联条目/概念（≤10），每对一句"为什么相关" + 可点路径。
3. 输出是**可解释的报告**，不悄悄删/链/挪。

## 1 · 找孤儿（可追溯）
1. **建反链索引**：扫 `wiki/`（`summaries`/`concepts`/`indexes`）里的 `[[条目]]`，建**入链表**（谁被链）。
2. **零入链** = 孤儿；"入链"含文件名、标题、内联 `[[双链]]`。
3. 用**文件名/标题**（不是模糊匹配）解析条目。

## 2 · 近关联配对（LLM + 检索）
给一个孤儿，找**值得连**的条目：
- **同概念/同主题**（共享关键术语、标签、实体）
- **直接/情境/证据**关系（`[[S-###]]` 来源也参与，不只 `wiki/`）
- **LLM 语义相似**（读内容，不只关键词）

每个孤儿 1–3 个近关联（≤10 组），**只挑真的**——不为凑数塞弱相关。

## 3 · 输出格式
```
孤儿笔记（零入链）：
  [条目名] — 文件路径
  ...
---
近关联：
  [孤儿条目] ←→ [近关联条目/概念]
    为什么相关（一句话）
    路径：wiki/...  路径：wiki/...
```
- **一条笔记给路径**（相对 `raw/`/`wiki/` 路径或 `[[wikilink]]`，不报 `obsidian://`）。
- **一对一句"为什么"**，不超过 10 组。

## 4 · 边界（不出声的不改）
- **绝不**自动删除、链接、移动孤儿。**可以**建议去向（`wiki/indexes/`、合适 `C-###`），要不要做由用户定。
- 只扫 `raw/`、`wiki/`，不越界到 `outputs/`、平台成品目录。
- 没有孤儿 / 没有近关联就说**没有**，不硬凑。
