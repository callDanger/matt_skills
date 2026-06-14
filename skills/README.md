# Skills

本仓库包含一组可复用、可组合的 AI 编码智能体技能模块。每个技能都是一个独立的目录，内含一个 `SKILL.md` 文件，定义了特定工作流或能力的说明、示例和/或参考材料。

技能按成熟度和用途分为以下几类：

| 分类 | 说明 | 数量 |
|------|------|-------|
| [`engineering/`](#engineering) | 日常编码工作使用的技能 | 10 |
| [`productivity/`](#productivity) | 通用工作流工具，不限于代码 | 4 |
| [`misc/`](#misc) | 不常用但保留的工具 | 4 |
| [`personal/`](#personal) | 与个人设置相关，不在插件中推广 | 2 |
| [`in-progress/`](#in-progress) | 仍在开发中的技能，可能有粗糙边缘 | 5 |
| [`deprecated/`](#deprecated) | 不再活跃使用的技能 | 4 |

**总计：29 个技能**

---

## Engineering

日常软件工程工作使用的技能。

- **[diagnose](./engineering/diagnose/SKILL.md)** — 针对疑难 Bug 与性能回退的纪律化诊断流程：复现 → 最小化 → 假设 → 插桩 → 修复 → 回归测试。
- **[grill-with-docs](./engineering/grill-with-docs/SKILL.md)** — 对照现有领域模型挑战你的计划，打磨术语，并即时更新 `CONTEXT.md` 和 ADR。
- **[improve-codebase-architecture](./engineering/improve-codebase-architecture/SKILL.md)** — 在代码库中寻找深化机会，参考 `CONTEXT.md` 中的领域语言和 `docs/adr/` 中的决策。
- **[prototype](./engineering/prototype/SKILL.md)** — 构建可丢弃的原型来充实设计——要么是一个可运行的终端应用来验证状态/业务逻辑问题，要么是一个路由下可切换的多种截然不同的 UI 变体。
- **[setup-matt-pocock-skills](./engineering/setup-matt-pocock-skills/SKILL.md)** — 搭建其他工程技能所需的仓库级配置（issue 跟踪器、分类标签词汇表、领域文档布局）。
- **[tdd](./engineering/tdd/SKILL.md)** — 测试驱动开发，采用红-绿-重构循环。一次一个垂直切片地构建功能或修复 Bug。
- **[to-issues](./engineering/to-issues/SKILL.md)** — 将任何计划、规格或 PRD 拆分为可按垂直切片独立承接的 GitHub issue。
- **[to-prd](./engineering/to-prd/SKILL.md)** — 将当前对话上下文转化为 PRD，并作为 GitHub issue 提交。
- **[triage](./engineering/triage/SKILL.md)** — 通过分类角色状态机对 issue 进行分类。
- **[zoom-out](./engineering/zoom-out/SKILL.md)** — 让智能体拉开距离，从不熟悉的代码段给出更宏观或更高层次的视角。

## Productivity

通用工作流工具，不限于写代码。

- **[caveman](./productivity/caveman/SKILL.md)** — 超压缩通信模式。通过去掉填充词，在保持完整技术准确性的同时，token 用量减少约 75%。
- **[grill-me](./productivity/grill-me/SKILL.md)** — 就一项计划或设计被无情地追问，直到决策树的每个分支都被理清。
- **[handoff](./productivity/handoff/SKILL.md)** — 将当前对话压缩成一份交接文档，让另一个智能体可以继续工作。
- **[write-a-skill](./productivity/write-a-skill/SKILL.md)** — 以正确的结构、渐进式披露和捆绑资源创建新技能。

## Misc

不常用但保留的工具。

- **[git-guardrails-claude-code](./misc/git-guardrails-claude-code/SKILL.md)** — 设置 Claude Code 钩子，在执行前拦截危险的 git 命令（push、reset --hard、clean 等）。
- **[migrate-to-shoehorn](./misc/migrate-to-shoehorn/SKILL.md)** — 将测试文件从 `as` 类型断言迁移到 @total-typescript/shoehorn。
- **[scaffold-exercises](./misc/scaffold-exercises/SKILL.md)** — 创建带有章节、问题、解答和讲解的练习目录结构。
- **[setup-pre-commit](./misc/setup-pre-commit/SKILL.md)** — 设置 Husky pre-commit 钩子，包含 lint-staged、Prettier、类型检查和测试。

## Personal

与个人设置相关的技能，不在插件中推广。

- **[edit-article](./personal/edit-article/SKILL.md)** — 通过重组章节、提升清晰度和精简文笔来编辑和润色文章。
- **[obsidian-vault](./personal/obsidian-vault/SKILL.md)** — 使用 wikilinks 和索引笔记在 Obsidian 笔记库中搜索、创建和管理笔记。

## In Progress

仍在开发中的技能。它们可能有粗糙边缘、破坏性变更或被放弃的实验，在毕业到稳定分类之前被排除在插件和顶层列表之外。

- **[review](./in-progress/review/SKILL.md)** — 从两个并行维度审查自固定点以来的变更：**标准**（diff 是否遵循仓库的编码标准？）和**规范**（diff 是否忠实地实现了原始 issue/PRD？）。
- **[teach](./in-progress/teach/SKILL.md)** — 在当前工作区内教授用户一项新技能或新概念。
- **[writing-beats](./writing-beats/SKILL.md)** — 像选择你自己的冒险一样，将文章塑造成一段节拍之旅。选择一个起始节拍，只写那一个节拍，然后转向下一个，直到文章自然结束。
- **[writing-fragments](./in-progress/writing-fragments/SKILL.md)** — 通过追问挖掘碎片——异质的写作金块——并将它们追加到一份文档中，作为未来文章的原材料。
- **[writing-shape](./in-progress/writing-shape/SKILL.md)** — 取一份原始材料的 markdown 文件，逐段塑造成文章，并在每一步论证格式选择。

## Deprecated

不再活跃使用的技能。

- **[design-an-interface](./deprecated/design-an-interface/SKILL.md)** — 使用并行子智能体为一个模块生成多个截然不同的接口设计。
- **[qa](./deprecated/qa/SKILL.md)** — 交互式 QA 会话，用户以对话方式报告 Bug，智能体提交 GitHub issue。
- **[request-refactor-plan](./deprecated/request-refactor-plan/SKILL.md)** — 通过用户访谈创建包含细小提交的详细重构计划，然后作为 GitHub issue 提交。
- **[ubiquitous-language](./deprecated/ubiquitous-language/SKILL.md)** — 从当前对话中提取 DDD 风格的统一语言词汇表。
