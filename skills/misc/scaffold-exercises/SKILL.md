---
name: scaffold-exercises
description: 创建包含章节、练习题、参考答案和讲解内容的练习目录结构，并确保通过 lint 检查。当用户想要搭建练习、创建练习模板或设置新课程章节时使用。
---

# 搭建练习

创建能通过 `pnpm ai-hero-cli internal lint` 的练习目录结构，然后使用 `git commit` 提交。

## 目录命名

- **章节**：`exercises/` 内的 `XX-section-name/`（例如：`01-retrieval-skill-building`）
- **练习**：章节内的 `XX.YY-exercise-name/`（例如：`01.03-retrieval-with-bm25`）
- 章节编号 = `XX`，练习编号 = `XX.YY`
- 名称使用短横线连接（小写，连字符）

## 练习变体

每个练习至少需要以下一个子文件夹：

- `problem/` - 学生练习区，包含 TODO
- `solution/` - 参考实现
- `explainer/` - 概念性内容，无 TODO

创建模板时，除非计划另有说明，否则默认使用 `explainer/`。

## 必需文件

每个子文件夹（`problem/`、`solution/`、`explainer/`）都需要一个 `readme.md`，要求：

- **不为空**（必须有实际内容，即使只有一行标题也可以）
- 无失效链接

创建模板时，用标题和描述生成最简 readme：

```md
# Exercise Title

Description here
```

如果子文件夹包含代码，还需要一个 `main.ts`（超过 1 行）。但对于模板，仅含 readme 的练习即可。

## 工作流程

1. **解析计划** - 提取章节名称、练习名称和变体类型
2. **创建目录** - 对每个路径执行 `mkdir -p`
3. **创建模板 readme** - 每个变体文件夹一个 `readme.md`，包含标题
4. **运行 lint** - 执行 `pnpm ai-hero-cli internal lint` 验证
5. **修复错误** - 迭代直到 lint 通过

## Lint 规则摘要

Linter（`pnpm ai-hero-cli internal lint`）检查以下内容：

- 每个练习都包含子文件夹（`problem/`、`solution/`、`explainer/`）
- `problem/`、`explainer/` 或 `explainer.1/` 至少存在一个
- 主子文件夹中存在且非空的 `readme.md`
- 无 `.gitkeep` 文件
- 无 `speaker-notes.md` 文件
- readme 中无失效链接
- readme 中无 `pnpm run exercise` 命令
- 除非仅含 readme，否则每个子文件夹都需要 `main.ts`

## 移动/重命名练习

重新编号或移动练习时：

1. 使用 `git mv`（而非 `mv`）重命名目录——保留 git 历史
2. 更新数字前缀以保持顺序
3. 移动后重新运行 lint

示例：

```bash
git mv exercises/01-retrieval/01.03-embeddings exercises/01-retrieval/01.04-embeddings
```

## 示例：根据计划创建模板

给定如下计划：

```
Section 05: Memory Skill Building
- 05.01 Introduction to Memory
- 05.02 Short-term Memory (explainer + problem + solution)
- 05.03 Long-term Memory
```

创建：

```bash
mkdir -p exercises/05-memory-skill-building/05.01-introduction-to-memory/explainer
mkdir -p exercises/05-memory-skill-building/05.02-short-term-memory/{explainer,problem,solution}
mkdir -p exercises/05-memory-skill-building/05.03-long-term-memory/explainer
```

然后创建 readme 模板：

```
exercises/05-memory-skill-building/05.01-introduction-to-memory/explainer/readme.md -> "# Introduction to Memory"
exercises/05-memory-skill-building/05.02-short-term-memory/explainer/readme.md -> "# Short-term Memory"
exercises/05-memory-skill-building/05.02-short-term-memory/problem/readme.md -> "# Short-term Memory"
exercises/05-memory-skill-building/05.02-short-term-memory/solution/readme.md -> "# Short-term Memory"
exercises/05-memory-skill-building/05.03-long-term-memory/explainer/readme.md -> "# Long-term Memory"
```
