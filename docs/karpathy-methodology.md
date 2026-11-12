# Karpathy「LLM Knowledge Bases」方法论 — 从 @yanhua1010/status/2039966047378583815 提取

> 来源：Yanhua 的 X Article《用 LLM + Obsidian 构建个人知识库：基于 Karpathy 的“LLM Knowledge Bases”工作流》(2026-04-03)
> 核心类比：**Obsidian Vault = 代码仓库，LLM = 编译器。** 把原始资料“编译”成结构化知识。

## 目录结构（原文代码块，entity key=5）
```
Vault/
├── raw/                    # 原始资料，不改
│   ├── articles/           # Web Clipper 剪藏
│   ├── podcasts/           # Podwise 导出
│   └── papers/             # 论文
│
├── wiki/                   # 编译产物，LLM 维护
│   ├── indexes/            # 索引（来源清单、概念清单、术语表）
│   ├── concepts/           # 概念条目
│   └── summaries/          # 逐篇摘要
│
├── outputs/                # 运行时输出
│   ├── qa/                 # 问答沉淀
│   └── health/             # 健康检查报告
│
├── x/                      # X 平台成品
├── 公众号/                  # 公众号成品
└── 小红书/                  # 小红书成品
```
注：原文正文另提到 X 推文/零散内容走“手动剪藏”入口入 raw；成品目录（x/公众号/小红书）给读者看，wiki/ 给自己看，两者不混。

## 软件工程 ↔ 知识库工程对照（entity key=3）
```
软件工程          →  知识库工程
src/             →  raw/（原始资料）
build/           →  wiki/（知识条目）
logs/            →  outputs/（问答归档）
编译器            →  LLM
IDE              →  Obsidian
Lint / CI        →  健康检查
增量编译          →  只处理新增/变更的 raw
```

## Q&A 输出模板（entity key=8，outputs/qa/ 落文件）
```markdown
---
question: "RAG 和轻量索引的适用边界？"
asked_at: 2026-04-03
sources:
  - [[S-001 MotherDuck Obsidian RAG]]
  - [[C-042 RAG]]
---
# RAG vs 轻量索引
## TL;DR
## 结论
## 证据（链接回原始来源）
## 不确定性
```
命名约定：`S-###` = source（来源条目），`C-###` = concept（概念条目）。

## 方法论硬原则
1. **编译 Compile**：raw→wiki 是“编译”，LLM 是编译器，不是随手摘要。
2. **分层**：原始资料 / 编译产物 / 运行时输出 三层分开，别混。
3. **增量**：只处理新增/变更的 raw，不全量重建。
4. **可追溯**：每个知识条目能追到原始来源，摘要保留原文引用（source_url/author/published/tags 元数据必填）。
5. **索引优先，别上 RAG**：<1万条靠 indexes/（All-Sources / All-Concepts / 术语表），LLM 先读索引定位再读原文。规模大了才考虑向量检索。
6. **Output 落文件**：每次复杂问答结果存 outputs/qa/，变成可复用知识条目（带推理+来源）。
7. **健康检查 Health Checks**：每周 outputs/health/，查①一致性（概念定义冲突）②完整性（缺定义/例子/来源）③孤岛（入链出链<2）。
8. **质量靠规范文件**（CLAUDE.md/AGENTS.md）：摘要模板、概念条目字段、命名规则，LLM 每次启动都读。

## 编译三件事（wiki 产物）
- 逐篇摘要 → wiki/summaries/（核心结论/关键证据/疑点/术语）
- 概念抽取 → wiki/concepts/（新概念建条目，老概念补证据）
- 索引更新 → wiki/indexes/（All-Sources / All-Concepts / 术语表）
