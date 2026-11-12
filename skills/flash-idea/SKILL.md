---
name: flash-idea
display_name: 闪念入库
display_name_en: Flash Idea Capture
description_zh: 把闪念/灵感/推文/链接存进记忆层：优先 flomo MCP，其次其它线上笔记 MCP，否则落本地 raw/flash-idea/。
description_en: Capture flash ideas, sparks, and links into the memory layer via flomo MCP, another online-note MCP, or local raw/flash-idea/ as fallback.
version: "1.0.0"
author: xiaohei_spring
description: Use when capturing a 闪念/灵感/推文/X link into the memory layer. Routes to flomo MCP, another online-note MCP, or local raw/flash-idea as fallback. Prefer this over any manual note-taking when the user drops an idea or link.
---

# flash-idea — 记忆层入口（L1 闪念 / 灵感 / 推文）

> 方法论角色：`raw/` 里的一手闪念。这是整个知识库的**记忆层**——最轻、最快、最碎的输入。
> 对照原文的「不要记笔记」：学习的第一步不是记，是让 agent 把闪念/推文**落地成结构化元数据**。

## 1. 三级写入路由（按顺序判定，命中即止）

| 优先级 | 条件 | 写入目标 | 动作 |
|--------|------|---------|------|
| ①  | 已接入 **flomo MCP** | flomo | 用 flomo 写入，**必带 `#闪念/Import` 标签**（存档/搜索用，正文不写） |
| ②  | 未接 flomo，但接了**其它线上笔记 MCP**（Notion / Obsidian Sync / Logseq / 语雀…） | 该线上笔记 | 写入其闪念/收件箱库，保留 `source:` 与 `[[S-###]]` 锚点 |
| ③  | **未接任何线上笔记 MCP**（默认兜底） | 本地 `raw/flash-idea/` | 按日聚合：`raw/flash-idea/<YYYY-MM-DD>.md`，一条一段 |

**路由判定**：先问清/探测当前 agent 会话连了哪些 MCP。连了 flomo 走 ①，否则连了别的线上笔记走 ②，都没有走 ③。**默认走 ③**（本地），除非用户明确说接了 MCP。

## 2. 入库内容与格式

一条闪念 = **一句带新信息的简介 + 裸原链接**（回源用）。

- **简介只写原帖没明说的信息**：这篇讲了什么、为什么值得记。
- **禁止只丢链接**、**禁止只贴原文**、**禁止编造链接里没有的经历**。
- **链接原样放**（`https://t.co/...`、`x.com/...` 不要改写/展开），作为 `source:` 锚点。
- **隐私红线**：情绪、焦虑、心理状态、语音日记原文**不入库**。真要留，必须用户逐字主动确认。

**推文 / X 链接格式**：
```
- <一句话：这篇讲了什么 / 为什么值得记>
  <原链接，原样>
  source: <原链接>
  tags: #闪念/Import
```

## 3. 索引行

每条入库后，在 `raw/flash-idea/` 顶部维护索引，格式：

```
- YYYY-MM-DD · 一句话简介 · [[S-### 或未编译]] · <链接>
```

被 `wiki/` 编译后，把占位换成对应 `[[S-###]]` / `[[C-###]]`。

## 4. 输出

写入成功后回一句：
```
已入库 <flomo / Notion / raw/flash-idea/2026-04-03.md>：<一句话简介> · <链接>
```
