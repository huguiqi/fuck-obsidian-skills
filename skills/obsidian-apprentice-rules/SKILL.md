---
name: obsidian-apprentice-rules
display_name: 编译规范
display_name_en: Compile Rules
description_zh: Karpathy 编译与写入规范 + 冲突裁定 + 保留红线；写库前先读。
description_en: Karpathy compile & write rules, conflict rulings, and guardrails to read before any vault write.
version: "1.0.0"
author: xiaohei_spring
description: Use before any write/compile into the knowledge base. Karpathy 编译与写入规范（分层 / 命名 / 增量 / 可追溯 / 健康检查）+ 保留的写入红线（file over app / 隐私 / 亲历门槛）。任何 raw→wiki 编译、笔记写入、对外草稿前必读。
---

# Karpathy 编译与写入规范

> 本文件是整个知识库的**编译规范**（原文里的 `CLAUDE.md`）。它是从 Kepano「apprentice 规则」改写而来——
> 凡与 Karpathy「LLM Knowledge Bases」冲突的，一律以 Karpathy 为准；不冲突的写入红线予以保留。

## 一、方法论内核（Karpathy 胜出）

**Obsidian 的 Vault 当代码仓库，LLM 当编译器，笔记是源码，把散点编译成结构化知识。**

对照表（原文照录）：

| 软件工程 | 知识库工程 |
|----------|-----------|
| `src/` | `raw/`（原始资料） |
| `build/` | `wiki/`（知识条目） |
| `logs/` | `outputs/`（问答归档） |
| 编译器 | LLM |
| IDE | Obsidian |
| Lint / CI | 健康检查 |
| 增量编译 | 只处理新增/变更的 raw |

七条心法：**编译 · 分层 · 增量 · 可追溯 · 索引优先 · Output 落文件 · 健康检查**。

## 二、硬约束（写入前必须满足）

1. **分层**：只写进对应层——`raw/`（原文/闪念）、`wiki/`（编译产物）、`outputs/`（运行时归档）。不跨层乱放。
2. **命名统一**：来源 `S-### 简短标题`、概念 `C-### 概念名`、术语 `T-### 术语`。文件名带 ID + 可读名。
3. **可追溯**：`wiki/` 与 `outputs/` 里的每条结论都 `[[S-###]]` / `[[C-###]]` 链回来源/概念，不写无源断言。
4. **原文不改**：`raw/` 只去噪（U+FFFC、空行、乱码），不改写、不摘要原文。
5. **File over app**：真 `.md` 文件、库内相对路径 + `[[wikilink]]`。**回报用文件路径，不用 `obsidian://` app 深链**。
6. **增量**：只编译 `raw/` 的新增/变更，不全库重跑。
7. **Output 落文件**：问答 / 健康报告写成 `outputs/` 里的 md，别只回聊天就丢。

## 三、编译动作（本规范授权 agent 替用户做）

> 原 Kepano 规则「不替用户理解、不把想法提升成结论」在**编译层面取消**——Karpathy 的核心就是让 LLM 把 raw 提升为 wiki。
> 但以下边界保留：

- ✅ **允许**：把 `raw/` 的原文/闪念**编译**成 `wiki/summaries`、`wiki/concepts`、`wiki/indexes`；补 `[[wikilink]]`；写 QA / 健康报告到 `outputs/`。
- ❌ **禁止（隐私红线）**：情绪、焦虑、心理状态、语音日记原文入库或编译。逐字确认才留。
- ❌ **禁止（个人信息红线）**：密码、手机号、token等能确定唯一身份的信息需要脱敏处理。

## 四、健康检查（每周，写到 `outputs/health/`）

| 检查项 | 抓什么 | 信号 | 去哪看 |
|--------|--------|------|--------|
| **一致性** | 新知识 vs 既有 `C-###` | 同概念 N 种说法、新定义打旧定义 | `wiki/concepts/` |
| **完整性** | 概念覆盖 | 重复 `S-###`、缺索引、缺反链 | `wiki/indexes/`、文件头 |
| **孤岛** | 连接密度 | 零双链的 `S-###`/`C-###` | `orphan-notes` 技能 |

不修复，只列出。修复走正常编译流程。

## 五、质量尺度

看**知识的可复用度**：概念是否说清本质、关联是否激活想法、问答能否追溯、边界是否明确、笔记是否在长。**不看数量，不看格式齐整。**
