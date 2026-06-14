---
name: grill-with-docs
description: 与你的计划进行对质，挑战它是否与现有领域模型一致，打磨术语，并在决策明确时即时更新文档（CONTEXT.md、ADR）。当用户希望根据项目的语言和已记录的决策对计划进行压力测试时使用。
---

<what-to-do>

就这个计划的每个方面对我进行无情追问，直到我们达成共识。沿着设计树的每个分支逐一走下去，逐个解决决策之间的依赖关系。每个问题都要给出你的推荐答案。

每次只问一个问题，等我对每个问题给出反馈后再继续。

如果某个问题可以通过探索代码库来回答，那就去探索代码库。

</what-to-do>

<supporting-info>

## 领域感知

在探索代码库时，也要查找现有文档：

### 文件结构

大多数仓库只有一个上下文：

```
/
├── CONTEXT.md
├── docs/
│   └── adr/
│       ├── 0001-event-sourced-orders.md
│       └── 0002-postgres-for-write-model.md
└── src/
```

如果根目录存在 `CONTEXT-MAP.md`，说明该仓库有多个上下文。该地图会指出每个上下文所在的位置：

```
/
├── CONTEXT-MAP.md
├── docs/
│   └── adr/                          ← system-wide decisions
├── src/
│   ├── ordering/
│   │   ├── CONTEXT.md
│   │   └── docs/adr/                 ← context-specific decisions
│   └── billing/
│       ├── CONTEXT.md
│       └── docs/adr/
```

按需创建文件——只有当你有内容可写时才创建。如果没有 `CONTEXT.md`，在第一个术语确定时创建一个。如果没有 `docs/adr/`，在需要第一个 ADR 时创建它。

## 会话期间

### 对照术语表挑战

当用户使用的术语与 `CONTEXT.md` 中现有语言冲突时，立即指出。"你的术语表将 'cancellation' 定义为 X，但你似乎指的是 Y——到底是哪个？"

### 明确模糊语言

当用户使用模糊或语义过载的术语时，提出一个精确的规范术语。"你说的是 'account'——你指的是 Customer 还是 User？它们是不同的东西。"

### 讨论具体场景

当讨论领域关系时，用具体场景对它们进行压力测试。设计一些探查边缘情况的场景，迫使用户明确概念之间的边界。

### 与代码交叉验证

当用户说明某事的运作方式时，检查代码是否一致。如果你发现矛盾，提出来："你的代码会取消整个 Orders，但你刚刚说可以 partial cancellation——哪个是对的？"

### 即时更新 CONTEXT.md

当一个术语确定下来时，立即更新 `CONTEXT.md`。不要把它们攒起来——要边确定边记录。使用 [CONTEXT-FORMAT.md](./CONTEXT-FORMAT.md) 中的格式。

`CONTEXT.md` 应该完全不含实现细节。不要把它当作 spec、草稿或实现决策的存放处。它只是一个术语表，仅此而已。

### 谨慎提供 ADR

只有当以下三点都成立时，才提议创建 ADR：

1. **难以回退** —— 日后改主意的代价很大
2. **没有上下文会显得奇怪** —— 未来的读者会疑惑 "为什么他们要这么做？"
3. **真正权衡的结果** —— 存在真正的替代方案，而你出于特定原因选择了其中一个

如果三条中任意一条不满足，就跳过 ADR。使用 [ADR-FORMAT.md](./ADR-FORMAT.md) 中的格式。

</supporting-info>
