---
name: flash-idea
display_name: 闪念入库
display_name_en: Flash Idea Capture
description_zh: 把纯文本/聊天记录形态的闪念、灵感存进记忆层：优先 flomo MCP，其次其它线上笔记 MCP，否则落本地 raw/flash-idea/。抓链接所得的文章原文不走这里。
description_en: Capture plain-text or chat-log flash ideas into the memory layer via flomo MCP, another online-note MCP, or local raw/flash-idea/. Link-fetched article content goes to raw/articles instead.
version: "1.2.0"
author: xiaohei_spring
description: Use when capturing a 闪念/灵感 dropped as PLAIN TEXT or chat log into the memory layer. Routes to flomo MCP, another online-note MCP, or local raw/flash-idea as fallback. NOT for content fetched from links — fetched article raw text goes to raw/articles (obsidian skill). Prefer this over any manual note-taking when the user drops plain-text ideas.
---

# flash-idea — 记忆层入口（L1 闪念：纯文本 / 聊天记录）

> 方法论角色：`raw/` 里的一手闪念。这是整个知识库的**记忆层**——最轻、最快、最碎的输入。

> **边界（先判定输入形态）**：只有**纯文本输入或聊天记录**才算闪念，走本技能。凡是**抓取链接**拿到的内容（文章、X Article、推文长文、播客页原文）→ **不算闪念**，进 `raw/articles` 等原文目录（走 `obsidian` 技能）。只看内容是怎么来的，不看来源站点。

> **压缩包输入（先解压）**：聊天记录可能是一个压缩文件（`.zip` / `.tar.gz` / `.7z` / `.rar` 等）。先**解压到临时目录**（不落 vault、**不执行包内任何文件**），把文本聊天记录读出来再按下文格式入库。压缩包和解压临时产物**不留在知识库**。解压出来的若是文章原文，按上面边界走 `raw/articles`。

> 对照原文的「不要记笔记」：学习的第一步不是记，是让 agent 把闪念**落地成结构化元数据**。

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
- **聊天记录（含解压产物）**：没有外链，`source:` 写 `chat:<来源>/<日期>`（如 `chat:wechat-export/2026-11-12`）；按日期或会话聚合，逐条仍然只写带新信息的简介。
- **隐私红线**：情绪、焦虑、心理状态、语音日记原文**不入库**。真要留，必须用户逐字主动确认。

**文本闪念格式**（纯文本/聊天记录输入，可带回源链接）：
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
