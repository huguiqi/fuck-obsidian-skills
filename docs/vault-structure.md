# Vault 目录结构（raw / wiki / outputs）

> **重要**：以下三层结构建立在**用户的 Obsidian Vault（知识库）里**，**不在本 skills 项目仓库里**。
> 本项目只提供**技能**（instructions），它们去**操作**用户 Vault 中的这些目录。
> 方法论出处：`docs/karpathy-methodology.md`。本文件是给 agent 参照的 Vault 结构约定。

---

## raw/ — 原始资料层（input，一般不改）

对应软件工程的 `src/`。只放**别人产出的原文**和**你自己的一手闪念**，按来源分子目录：

| 目录 | 内容 | 进入方式 |
|------|------|---------|
| `articles/` | 文章、博客、长文 | Web Clipper 剪藏 / `obsidian` 剪藏技能 |
| `podcasts/` | 播客、演讲、视频 | Podwise 导出 / `obsidian` 剪藏技能 |
| `papers/` | 论文 | 手动 / `obsidian` 剪藏技能 |
| `flash-idea/` | **闪念、灵感、推文**（记忆层兜底） | `flash-idea` 技能路由 |

**规矩**
- **原文不改**：只允许去噪（U+FFFC、空行、乱码），不改写、不摘要。
- **一手闪念**可直接进 `flash-idea/`，一条一个文件或按日聚合（`flash-idea/2026-04-03.md`）。
- 命名：来源文件名用 `S-### 简短标题.md`（见 `obsidian-apprentice-rules` ID 规范）。
- 每个 raw 文件必须留 `source:` 原始 URL，作为 `[[S-###]]` 的锚点。

**增量边界**：只处理新增/变更的 raw 文件，别推倒重编。

---

## wiki/ — 编译产物层（compiled，LLM 维护）

对应软件工程的 `build/`。由 `raw/` **编译**而来，是知识库的主体：

| 目录 | 内容 | 形态 |
|------|------|------|
| `summaries/` | 逐篇摘要 | `S-### 标题.md`，含 TL;DR / 金句 / 可复用观点 |
| `concepts/` | 概念条目 | `C-### 名称.md`，含定义 / 正文 / 来源 |
| `indexes/` | 索引 | 来源清单 `All-Sources`、概念清单 `All-Concepts`、术语表 `All-Terms` |

**编译原则**
- **激活 raw 里的知识**：把散点编译成结构化概念 + 关联索引 + 问答索引。
- **保留来源、不过度改写**：结论必须能追回 `[[S-###]]` 原文。
- **命名统一**：来源 `S-###`、概念 `C-###`、术语 `T-###`（见 `obsidian-apprentice-rules` 编译规范）。
- **双向链接**：概念 ↔ 摘要 ↔ 来源之间用 `[[wikilink]]` 互链，构成知识网。

**增量边界**：只重编新增/变更的 raw 对应的 wiki 产物。

---

## outputs/ — 运行时输出层（runtime output）

对应软件工程的 `logs/`。都是**运行时生成的归档**，不进知识网主体：

| 目录 | 内容 | 形态 |
|------|------|------|
| `qa/` | 问答沉淀 | `outputs/qa/<slug>.md`，含 frontmatter / TL;DR / 结论 / 证据 / 不确定性 |
| `health/` | 健康检查报告 | `outputs/health/<week>.md`，一致性 / 完整性 / 孤岛 |

**约定**：Output 落文件——问答结论写进 `outputs/qa/`，不只停在聊天窗。每周健康检查报告写进 `outputs/health/`。

---

## 平台成品（Vault 内独立目录）

`x/`、`公众号/`、`小红书/` 等**平台成品**放在 Vault（不在本项目）。成品是给读者看的，wiki 是给自己看的，两者不混。
