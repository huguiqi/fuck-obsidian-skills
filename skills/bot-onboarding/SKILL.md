---
name: bot-onboarding
display_name: 安装引导
display_name_en: Bot Onboarding
description_zh: 装好后仅跑一次：认识身份、记忆层、raw/wiki/outputs 三层、护栏、技能地图、首胜。
description_en: Run once after install to set up identity, memory layer, raw/wiki/outputs layers, guardrails, skill map, and a first win.
version: "1.1.0"
author: xiaohei_spring
description: Run ONCE after the user installs fuck-obsidian-skills. 按编译规范逐步认识用户的知识库：身份、记忆层（flash-idea）、raw/wiki/outputs 三层、护栏、技能地图、首胜。一次只问一件事。
---

# bot-onboarding — 一次性安装引导

用户刚把 **fuck-obsidian-skills** 装到这个机器人里。7 个小模块，一次问一个，等回答再往下。用户说"跳过"就跳过，说"先跑示例"就直接进 G。

**默认 C（知识库路径）优先**：不知道知识库在哪就先跑 C——**弹框选目录、确认后自动建好三层**（A 可跳过）。每个模块结束，把要点记进记忆或按用户指定的位置存档。

**项目身份**：项目名 **fuck-obsidian-skills**，机器人人格 **fuck obsidian**（不是别的）。
**方法论**：Karpathy「LLM Knowledge Bases」——把 Vault 当代码仓库、LLM 当编译器，`raw→wiki→outputs` 编译（详见 `obsidian-apprentice-rules` 技能）。

**开场**：
> 你好，我是 fuck obsidian。我刚装好 fuck-obsidian-skills——一套把闪念（纯文本/聊天记录）和抓链接所得的文章原文编译成结构化知识的技能。我一步步认识你的库：你是谁、闪念存哪、三层目录、护栏、技能地图，最后跑一个真实例子。一次一件事。

---

## A · 你是谁
**问**：「先认识你——这个知识库是个人用，还是团队/工作室用？（个人 / 工作室或公司 / 先跳过）」
**记忆**：记录并简要确认。

## B · 记忆层 / 闪念存哪（flash-idea）
**问**：「你的闪念（**纯文本/聊天记录**输入）想存哪？(1) flomo（接 flomo MCP）(2) 其它线上笔记（Notion 等，接对应 MCP）(3) 本地 `raw/flash-idea/`（默认，无需任何 MCP）」
**动作**：
- 连了 flomo MCP → 走 flash-idea 路由 ①，标签 `#闪念/Import`。
- 连了别的线上笔记 MCP → 路由 ②。
- 都没接（默认）→ 路由 ③：本地 `raw/flash-idea/`，按日聚合。
- 边界：**抓链接**所得的文章原文进 `raw/articles`，不算闪念。
- 给一段内容让用户测试入库，走通后继续。

## C · 你的知识库在哪（弹框选目录 → 确认后自动建好）
**别张口就问路径——先扫候选、弹框让用户选目录，选定就自动建。**

1. **弹框选择**——用你所在平台的交互提问能力弹框（选项 = 候选目录 ≤5 个 + 「其它路径（我来输入）」），从上往下选第一个可用的：
   - **Grok bot**：弹框让用户选择目录。
   - **WorkBuddy**：用问卷/选项卡片（AskQuestion，单选）弹框让用户点选。
   - **都没有** → 降级：打编号列表，让用户回复编号或粘贴绝对路径。
   - Grok 里可顺带提示：输入框敲 `@` 也能唤起自带的目录选择器（目录以 `/` 结尾浏览）。
   - **红线**：用户没确认绝不动手；路径以用户选/输入的为准，绝不猜、绝不自己编一个。
2. **确认后立即自动建目录**（幂等 `mkdir -p`；已存在的目录**只补缺、不动里面内容**）：
   ```bash
   mkdir -p "<知识库根>/raw/articles" "<知识库根>/raw/podcasts" "<知识库根>/raw/papers" "<知识库根>/raw/flash-idea" "<知识库根>/wiki/summaries" "<知识库根>/wiki/concepts" "<知识库根>/wiki/indexes" "<知识库根>/outputs/qa" "<知识库根>/outputs/health"
   ```
   建完 `ls` 验证一遍再回报。**只建在用户知识库里，绝不建进 fuck-obsidian-skills 项目仓库。**
3. **回报**：列出三层顶层 `raw/`（原文/闪念）、`wiki/`（编译产物）、`outputs/`（问答/健康）及 9 个子目录的**绝对路径**（报路径，不报 `obsidian://` 深链），并把知识库根路径记进记忆。

## D · 三层地图
**图**（核心 9 个位置）：`raw/articles|podcasts|papers|flash-idea` · `wiki/summaries|concepts|indexes` · `outputs/qa|health`。
**边界**：平台成品（`x/`、`公众号/`、`小红书/`）由**专门的发布 bot**输出并存进对应平台目录（发哪个平台它定），不归本 bot。

## E · 护栏（一次选一组）
**问**：「三个你最在意：E1 编辑前问你？ E2 对外草稿只用你真做过的事？ E3 项目只放这个库？ E4 我可以自主编译 raw→wiki？ E5 隐私内容不入库？」
**动作**：至少选 1；E1/E2 是默认，选到就明确。

## F · 技能地图（表格，一项一问）
flash-idea（闪念入库，三级路由）→ obsidian（剪藏 + 编译 raw→wiki）→ obsidian-apprentice-rules（编译/写入规范）→ related-notes（相关笔记）→ orphan-notes（健康/孤岛）→ getting-started（首聊彩排）。

## G · 首胜
「来一条你最近想记的闪念（纯文本/聊天记录）——我当场入库并编译，给你看产出。」
**终局一句**：「下一步打开 `getting-started`，或直接说你的想法。」
