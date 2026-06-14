---
name: setup-matt-pocock-skills
description: 在 AGENTS.md/CLAUDE.md 中设置 `## Agent skills` 区块，并在 `docs/agents/` 中创建配套文档，使工程类技能了解本仓库的 issue tracker（GitHub 或本地 markdown）、triage 标签词汇表以及领域文档布局。在首次使用 `to-issues`、`to-prd`、`triage`、`diagnose`、`tdd`、`improve-codebase-architecture` 或 `zoom-out` 之前运行——或者当这些技能看起来缺少关于 issue tracker、triage 标签或领域文档的上下文时运行。
disable-model-invocation: true
---

# 设置 Matt Pocock 的技能

搭建工程类技能所依赖的、每个仓库的配置：

- **Issue tracker** —— issues 保存在哪里（默认为 GitHub；本地 markdown 也开箱即用）
- **Triage labels** —— 五个标准 triage 角色所使用的字符串
- **Domain docs** —— `CONTEXT.md` 与 ADR 的位置，以及阅读它们的消费者规则

这是一个 prompt-driven 的技能，而非确定性脚本。先探索，再展示发现，与用户确认，然后写入。

## 流程

### 1. 探索

查看当前仓库以了解其初始状态。读取任何已存在的内容；不要假设：

- `git remote -v` 和 `.git/config` —— 这是 GitHub 仓库吗？是哪个仓库？
- 仓库根目录下的 `AGENTS.md` 和 `CLAUDE.md` —— 是否存在？其中是否已有 `## Agent skills` 章节？
- 仓库根目录下的 `CONTEXT.md` 和 `CONTEXT-MAP.md`
- `docs/adr/` 以及任何 `src/*/docs/adr/` 目录
- `docs/agents/` —— 本技能之前的输出是否已存在？
- `.scratch/` —— 本地 markdown issue tracker 约定已在使用的迹象

### 2. 展示发现并询问

总结哪些已存在、哪些缺失。然后**一次一个**地引导用户完成三个决策 —— 展示一个章节，得到用户回答，再进入下一个。不要一次性抛出全部三个。

假设用户不知道这些术语的含义。每个章节开头先给出一个简短说明（它是什么、为什么这些技能需要它、选择不同会有什么变化）。然后展示选项和默认值。

**章节 A —— Issue tracker。**

> 说明："Issue tracker" 是本仓库 issues 存放的地方。`to-issues`、`triage`、`to-prd` 和 `qa` 等技能会读取并写入它——它们需要知道是调用 `gh issue create`、在 `.scratch/` 下写入 markdown 文件，还是遵循你描述的其他工作流。选择你实际用于跟踪本仓库工作的地方。

默认立场：这些技能为 GitHub 设计。如果 `git remote` 指向 GitHub，则建议使用它。如果 `git remote` 指向 GitLab（`gitlab.com` 或自托管主机），则建议使用 GitLab。否则（或用户更倾向的），提供：

- **GitHub** —— issues 保存在该仓库的 GitHub Issues 中（使用 `gh` CLI）
- **GitLab** —— issues 保存在该仓库的 GitLab Issues 中（使用 [`glab`](https://gitlab.com/gitlab-org/cli) CLI）
- **Local markdown** —— issues 以文件形式保存在本仓库的 `.scratch/<feature>/` 下（适合个人项目或没有 remote 的仓库）
- **Other**（Jira、Linear 等）—— 请用户用一段话描述工作流；本技能会将其记录为自由格式文本

**章节 B —— Triage label vocabulary。**

> 说明：当 `triage` 技能处理新 issue 时，它会通过一个状态机流转——需要评估、等待报告者回复、可供 AFK agent 接手、需要人工处理，或不会修复。为此，它需要应用与你实际配置相匹配的标签（或 issue tracker 中的等价物）。如果你的仓库已使用不同的标签名称（例如用 `bug:triage` 而不是 `needs-triage`），请在此处映射，以免本技能创建重复标签。

五个标准角色：

- `needs-triage` —— 维护者需要评估
- `needs-info` —— 等待报告者回复
- `ready-for-agent` —— 已完全明确，可 AFK 接手（agent 无需人工上下文即可接手）
- `ready-for-human` —— 需要人工实现
- `wontfix` —— 不会处理

默认：每个角色的字符串与其名称相同。询问用户是否想覆盖任何一项。如果其 issue tracker 尚无现有标签，默认值即可。

**章节 C —— Domain docs。**

> 说明：某些技能（`improve-codebase-architecture`、`diagnose`、`tdd`）会读取 `CONTEXT.md` 以了解项目的领域语言，并读取 `docs/adr/` 以了解过往架构决策。它们需要知道仓库是只有一个全局上下文，还是有多个上下文（例如前后端分离的 monorepo），以便在正确位置查找。

确认布局：

- **Single-context** —— 仓库根目录下只有一个 `CONTEXT.md` + `docs/adr/`。大多数仓库属于此类。
- **Multi-context** —— 根目录下有 `CONTEXT-MAP.md`，指向每个上下文的 `CONTEXT.md` 文件（通常是 monorepo）。

### 3. 确认并编辑

向用户展示以下草稿：

- 要添加到 `CLAUDE.md` / `AGENTS.md` 中正在编辑文件里的 `## Agent skills` 区块（选择规则见第 4 步）
- `docs/agents/issue-tracker.md`、`docs/agents/triage-labels.md`、`docs/agents/domain.md` 的内容

允许他们在写入前编辑。

### 4. 写入

**选择要编辑的文件：**

- 如果 `CLAUDE.md` 存在，编辑它。
- 否则如果 `AGENTS.md` 存在，编辑它。
- 如果两者都不存在，询问用户要创建哪一个——不要替他们选择。

当 `CLAUDE.md` 已存在时，切勿创建 `AGENTS.md`（反之亦然）—— 始终编辑已存在的那个。

如果所选文件中已存在 `## Agent skills` 区块，就原地更新其内容，而不是追加重复内容。不要覆盖用户对周围章节的编辑。

该区块：

```markdown
## Agent skills

### Issue tracker

[where issues are tracked 的单行摘要]. 参见 `docs/agents/issue-tracker.md`.

### Triage labels

[label vocabulary 的单行摘要]. 参见 `docs/agents/triage-labels.md`.

### Domain docs

[布局的单行摘要 —— "single-context" 或 "multi-context"]. 参见 `docs/agents/domain.md`.
```

然后根据本技能文件夹中的种子模板，写入三个文档文件：

- [issue-tracker-github.md](./issue-tracker-github.md) —— GitHub issue tracker
- [issue-tracker-gitlab.md](./issue-tracker-gitlab.md) —— GitLab issue tracker
- [issue-tracker-local.md](./issue-tracker-local.md) —— 本地 markdown issue tracker
- [triage-labels.md](./triage-labels.md) —— label 映射
- [domain.md](./domain.md) —— 领域文档消费者规则 + 布局

对于 "other" issue tracker，根据用户的描述从头编写 `docs/agents/issue-tracker.md`。

### 5. 完成

告诉用户设置已完成，以及哪些工程类技能现在会读取这些文件。说明他们以后可以直接编辑 `docs/agents/*.md` —— 只有当他们想切换 issue tracker 或从头开始时，才需要重新运行本技能。
