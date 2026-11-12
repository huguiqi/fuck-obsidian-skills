<p align="center">
  <img src="assets/social-preview.png" alt="fuck-obsidian-skills banner" width="100%">
</p>

# fuck-obsidian-skills

把 LLM 变成你的**知识库编译器**：闪念/推文先进记忆层，再编译成结构化知识。
一套遵循 [Agent Skills 规范](https://agentskills.io/specification) 的技能包，落地 Andrej Karpathy 的「LLM Knowledge Bases」方法论——**把 Vault 当代码仓库、LLM 当编译器、笔记当源码。**

> 项目名：**fuck-obsidian-skills** · 机器人名：**fuck obsidian**

## 🎯 给谁用

优先面向 **Grok bot**（xAI）与 **WorkBuddy**（腾讯）两类 agent 平台，也兼容任何遵循 Agent Skills `SKILL.md` 标准的 agent（Cursor、Claude Code 等）。

| 平台 | 匹配情况 | 说明 |
|------|---------|------|
| **Grok bot** | ✅ 开箱即用 | `skills/<name>/SKILL.md` + `name`/`description` 即为 Grok 规范；多余的 key Grok 自动忽略 |
| **WorkBuddy** | ✅ 已补齐必填字段 | 额外补了 `display_name`/`display_name_en`/`description_zh`/`description_en`/`version`/`author`，目录名 = `name` |

## 🧩 技能地图

| Id | name | 用途 |
|----|------|------|
| 一次性安装引导 | `bot-onboarding` | **仅安装后第一次**跑：认识身份、记忆层、三层目录、护栏、技能地图、首胜 |
| 首次对话彩排 | `getting-started` | 每次首次对话跑这个：入门 + 跑通一条闪念入库+编译 |
| 闪念入库 | `flash-idea` | **记忆层**：闪念/灵感/推文（flomo MCP / 其它线上笔记 MCP / 本地 `raw/flash-idea/`） |
| 剪藏编译 | `obsidian` | 批量剪藏文章/播客/论文，抓全文并编译 raw→wiki（摘要/概念/索引） |
| 编译规范 | `obsidian-apprentice-rules` | Karpathy 编译与写入规范 + 冲突裁定 + 保留红线（写库前先看） |
| 关联笔记 | `related-notes` | 分享一个想法 → 在 raw/wiki 找 ≤5 条相关笔记（一条一句"为什么"+ 路径） |
| 孤岛检查 | `orphan-notes` | 孤儿笔记/健康检查：零双链 + 近关联配对（默认只读） |

## 🗂 Vault 目录结构（技能操作的目标）

> ⚠️ 这套 `raw/wiki/outputs` 三层结构建在**用户的 Obsidian Vault（知识库）里**，**不在本项目仓库里**。
> 本项目只提供技能去操作 Vault。详见 `docs/vault-structure.md`。

```
Vault/
├── raw/                    # 原始资料层（input，不改）—— src/
│   ├── articles/  podcasts/  papers/
│   └── flash-idea/         # 闪念/灵感/推文（记忆层本地兜底）
├── wiki/                   # 编译产物层（compiled，LLM 维护）—— build/
│   ├── summaries/  concepts/  indexes/
├── outputs/                # 运行时输出层（runtime）—— logs/
│   ├── qa/  health/
└── x/  公众号/  小红书/     # 平台成品（给读者看，与 wiki 不混）
```

**编译七心法**：编译 · 分层 · 增量 · 可追溯 · 索引优先（别上 RAG）· Output 落文件 · 每周健康检查。

## 📦 本项目仓库结构

```
fuck-obsidian-skills/
├── skills/          # agent 技能（Grok bot / WorkBuddy 读取）
├── docs/            # 方法论出处 · 编译规范 · Vault 结构
├── README.md  LICENSE
└── assets/          # 品牌图
```

## ⬇️ 安装

**通用（Agent Skills 标准）** — 把 `skills/` 下每个技能目录放进目标 agent 的技能目录：

**Grok bot**：把各技能目录拷到 `~/.grok/skills/`（个人）或 `<repo>/.grok/skills/`（项目）。

**WorkBuddy**：把各技能目录拷到 `~/.workbuddy/skills/`，`/reload-skills` 后生效（目录名须 = `name` 字段）。

**命令行**：

```sh
npx skills add huguiqi/fuck-obsidian-skills
```

> 装好后 → 让 agent 跑 `bot-onboarding`（一次性安装引导），一次问一件事。

## 📄 License

MIT © fuck-obsidian-skills contributors

---

## 🎨 品牌图

| 文件 | 尺寸 | 用途 |
|------|------|------|
| `assets/social-preview.png` | 2560×1280 | 顶部 banner（高清） |
| `assets/social-preview-1280x640.png` | 1280×640 | GitHub 社交卡 |

<img src="assets/social-preview-1280x640.png" alt="social card" width="60%">

---

### 🧠 为什么要做

信息爆炸，收集 ≠ 知识。这套方法论把「存储」改成「编译」——LLM 帮你编译，你负责思考。
Flash Layer 提速、双链织网、口径统一、产出有依据、按需交付、长期复利。

**方法论出处**：Andrej Karpathy「LLM Knowledge Bases」[Karpathy LLM Knowledge Bases文章](https://x.com/karpathy/status/2039805659525644595)。

经由 [Yanhua 的实践文章](https://x.com/yanhua1010/status/2039966047378583815)落地。本技能包是那套方法论的一个可复用实现。
