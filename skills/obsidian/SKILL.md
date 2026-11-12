---
name: obsidian
display_name: 剪藏编译
display_name_en: Clip & Compile
description_zh: 批量剪藏文章/播客/论文，抓全文并编译 raw→wiki（摘要/概念/索引）。
description_en: Clip and ingest articles, podcasts, and papers in bulk, then compile raw→wiki (summaries, concepts, indexes).
version: "1.0.0"
author: xiaohei_spring
description: Use when the user wants to clip/ingest a batch of articles, talks, podcasts, or videos into the knowledge base and COMPILE them raw→wiki per Karpathy. 抓全文 + 逐篇摘要 wiki/summaries + 概念 wiki/concepts + 索引 wiki/indexes + 抽检质量门。
---

# obsidian — 剪藏 + 编译（raw → wiki）

> 方法论角色：`raw/` 进料 + `wiki/` 编译。这是 Karpathy「编译器」的主入口。
> 范围：批量、项目制、真抓全文。单篇随手记（**纯文本/聊天记录**输入）走 `flash-idea`（记忆层）；写入规范见 `obsidian-apprentice-rules`。

## 0 · 两个禁令（不问，别做）
1. **不做无来源编译**：没抓到原文 / 缺 `source:` URL，就不编译进 wiki——先补来源，否则**列缺口**。
2. **不复述 / 不编造**：摘要提炼新信息，禁止把原文复读回去，禁止编造用户没做过的事（对外草稿尤其）。

## 1 · 范围（v1）
**凡是抓取链接拿到的文章原文**都进 raw/：文章、博客、X Article、推文长文 → `raw/articles`；播客、演讲、长视频 → `raw/podcasts`；论文 → `raw/papers`。**判定看输入形态，不看来源站点**。**不抓**：纯文本/聊天记录形态的闪念（→ `flash-idea`）。

## 2 · 进料 raw/
1. 逐条抓全文 + 去噪（U+FFFC、空行、乱码）。**原文不改写**。
2. 文件名 `raw/<来源>/S-### 简短标题.md`，带 frontmatter（`source:`、`published:`、`tags:`）。
3. **来源 URL 原样保真**（t.co 不展开）。

## 3 · 编译 wiki/
逐篇 `S-###`：
- **`wiki/summaries/S-### 标题.md`**：TL;DR（≤120字）· 金句（1–2）· 可复用观点（正文里挑真被引用/强化的）· 来源。
- **概念 `wiki/concepts/C-### 概念名.md`**（≥2 个概念）：一句话定义 / 来源反链 `[[S-###]]` / 术语 `[[T-###]]` / 原文里的应用 / 边界（不够格就别建，建就要链接密度）。
- **关联**：概念 ↔ 摘要 ↔ 来源用 `[[wikilink]]` 互链。

## 4 · 索引 wiki/indexes/
- **`All-Sources.md`**：`S-### · 标题 · 金句 · [[概念]] · source`
- **`All-Concepts.md`**：`C-### · 概念名 · 一句话定义`

## 5 · 质量门
7 天内**不主动抽检**。要质量再查（抽 3 条，记案）：
1. 概念像**摘要**还是**洞见**（≥80% 洞见）；
2. 相似概念的差异说清了吗；
3. 概念**互相链接了吗**。

## 6 · 输出
按批次回：剪了多少 · 逐篇 → 概念 → 索引，报**文件路径**（不报 `obsidian://`）。
格式：`S-###` 标题 → TL;DR · 金句 · 概念 · 源文件路径 · 全文路径。
