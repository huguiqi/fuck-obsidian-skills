---
name: Obsidian 批量剪藏
description: >-
  Use when bulk-clipping articles/posts into an Obsidian vault (X Articles,
  blogs, threads) with full text, wikilinks, MOCs, and optional bilingual notes.
---
# Obsidian 批量剪藏

给任意 agent：按来源列表批量做成可入库的 Markdown 笔记。验收=干成的真事（全文 + 可点的双链），不是概念说明。

## 输入（开跑前对齐）
- 来源列表：作者 / 平台 / URL 或已抓正文
- 目标库路径（由调度方或 Obsidian 专责写入；本技能只规定笔记形态）
- 落盘目录：别人写的原文 → `Clippings/`；AI 整理/双语/概念/MOC → `AI outputs/<任务名>/`
- 外文是否要双语（默认：英文长文要 `## English` + `## 中文` 完整译文）

## 每篇笔记必须长这样
```markdown
---
title: "..."
author: ...
date: YYYY-MM-DD
type: article|long-post|clipping
source: https://...
concepts:
  - "[[概念A]]"
  - "[[概念B]]"
---

# 标题

（可选封面图）

## English
（外文原文；若本来就是中文可省略本节，正文直接写）

## 中文
（完整译文，禁止一两句摘要）

## Concepts
- [[概念A]]
- [[概念B]]
```

## 硬规矩
1. **全文**：禁止摘要壳、禁止「Full text on X / 见原文」代替正文
2. **双链**：概念一律 `[[概念名]]`；每个概念笔记内用 `- [[文章笔记名]]` 回链；禁止纯词串 Concepts
3. **少文件夹**：批量任务内笔记尽量同层；导航靠 `00-Index`、作者 MOC、概念笔记的 `[[ ]]`，不靠层层目录
4. **不为断链批量建空壳**；未解析的 `[[链接]]` 可留作面包屑
5. **重大删除 / 批量挪动先请示**
6. 打包给 macOS 时用 `.tar.gz` 或 UTF-8 flag 的 zip（中文文件名）

## 批量步骤
1. 抓取/清洗正文（去 U+FFFC、段落空行、保留列表表格）
2. 需要则全文翻译，写入同一笔记双语区
3. 从正文抽 3–12 个稳定概念（去掉「问题/时间/价值」类万能噪音词），建/更新概念笔记与回链
4. 更新作者 MOC 与 `00-Index.md`
5. **抽检**：随机开 1 篇——正文够长、文末有 `[[ ]]`、概念页有反向链接；不过则整批重做该篇，不许带病入库
6. 交付：目录路径或 Mac 可解压缩包；并附一篇抽检笔记名

## 不要做
- 不要只交 public stub / 引用块
- 不要把 Concepts 写成无括号词云
- 不要未经允许写入用户 Obsidian 库根以外的私人笔记区；库操作交 Obsidian 专责或按用户当场指示
