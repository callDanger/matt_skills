---
name: obsidian-vault
description: 在 Obsidian 笔记库中搜索、创建和管理带有 wikilink 与索引笔记的笔记。当用户希望在 Obsidian 中查找、创建或整理笔记时使用。
---

# Obsidian 笔记库

## 笔记库位置

`/mnt/d/Obsidian Vault/AI Research/`

大部分笔记位于根目录下。

## 命名规范

- **索引笔记**：聚合相关主题（例如 `Ralph Wiggum Index.md`、`Skills Index.md`、`RAG Index.md`）
- 所有笔记名称使用**标题大写格式**
- 不使用文件夹来组织——改用链接和索引笔记

## 链接

- 使用 Obsidian `[[wikilinks]]` 语法：`[[Note Title]]`
- 笔记在底部链接到依赖或相关笔记
- 索引笔记就是 `[[wikilinks]]` 的列表

## 工作流

### 搜索笔记

```bash
# 按文件名搜索
find "/mnt/d/Obsidian Vault/AI Research/" -name "*.md" | grep -i "keyword"

# 按内容搜索
grep -rl "keyword" "/mnt/d/Obsidian Vault/AI Research/" --include="*.md"
```

或者直接对笔记库路径使用 Grep/Glob 工具。

### 创建新笔记

1. 文件名使用**标题大写格式**
2. 按照笔记库规则，将内容写成一个学习单元
3. 在底部添加指向相关笔记的 `[[wikilinks]]`
4. 如果属于编号序列，请使用层级编号方案

### 查找相关笔记

在笔记库中搜索 `[[Note Title]]` 以查找反向链接：

```bash
grep -rl "\\[\\[Note Title\\]\\]" "/mnt/d/Obsidian Vault/AI Research/"
```

### 查找索引笔记

```bash
find "/mnt/d/Obsidian Vault/AI Research/" -name "*Index*"
```
