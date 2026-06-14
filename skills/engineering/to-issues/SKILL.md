---
name: to-issues
description: 使用 tracer-bullet 垂直切片，将计划、规格说明书或 PRD 拆分为 issue 追踪器上可独立承接的 issue。当用户希望将计划转化为 issue、创建实现工单或拆解工作时使用。
---

# 拆分为 Issues

使用垂直切片（tracer bullets）将计划拆分为可独立承接的 issue。

issue 追踪器和 triage 标签词汇应当已经提供给你——如果没有，请运行 `/setup-matt-pocock-skills`。

## 流程

### 1. 收集上下文

从当前对话上下文中已有的信息开始工作。如果用户以参数形式传入了一个 issue 引用（issue 编号、URL 或路径），请从 issue 追踪器中获取并阅读其完整正文与评论。

### 2. 探索代码库（可选）

如果你尚未探索代码库，请进行探索以了解代码当前状态。issue 标题和描述应使用项目领域术语词汇表，并尊重你所触及区域内的 ADR。

### 3. 起草垂直切片

将计划拆分为 **tracer bullet** issue。每个 issue 都是一个贯穿所有集成层、端到端的薄垂直切片，而不是某一层上的水平切片。

切片可分为「HITL」或「AFK」。HITL 切片需要人工介入，例如架构决策或设计评审。AFK 切片无需人工介入即可实现并合并。在可能的情况下优先选择 AFK。

<vertical-slice-rules>
- 每个切片都要交付一条狭窄但贯穿每一层（schema、API、UI、测试）的完整路径
- 完成后的切片可以独立演示或验证
- 优先选择多个薄切片，而非少量厚切片
</vertical-slice-rules>

### 4. 与用户确认

将拟定的拆分以编号列表形式呈现。每个切片展示：

- **Title**: 简短描述性名称
- **Type**: HITL / AFK
- **Blocked by**: 哪些其他切片（如有）必须先完成
- **User stories covered**: 这解决了哪些用户故事（如果源材料中有）

询问用户：

- 粒度是否合适？（太粗 / 太细）
- 依赖关系是否正确？
- 是否有切片需要合并或进一步拆分？
- HITL 和 AFK 的标记是否正确？

迭代直到用户批准该拆分。

### 5. 将 issue 发布到 issue 追踪器

对于每个经批准的切片，在 issue 追踪器中发布一个新 issue。使用下方的 issue 正文模板。这些 issue 被认为已可供 AFK agent 承接，因此除非另有指示，否则请以正确的 triage 标签发布。

按依赖顺序发布 issue（阻塞项优先），以便你可以在「Blocked by」字段中引用真实的 issue 标识符。

<issue-template>
## Parent

issue 追踪器上父 issue 的引用（如果源内容本身就是一个现有 issue，则省略此部分）。

## What to build

对该垂直切片的简洁描述。描述端到端行为，而不是逐层实现。

避免特定文件路径或代码片段——它们很快就会过时。例外：如果原型产出的片段能比文字更精确地表达决策（状态机、reducer、schema、类型结构），请将其内联于此，并简要注明它来自原型。只保留富含决策信息的关键部分——不是可运行 demo，只是要点。

## Acceptance criteria

- [ ] 验收标准 1
- [ ] 验收标准 2
- [ ] 验收标准 3

## Blocked by

- 阻塞工单的引用（如有）

如果没有阻塞项，则填写「None - can start immediately」。

</issue-template>

不要关闭或修改任何父 issue。
