---
name: qa
description: 交互式 QA 会话，用户以对话方式报告 bug 或问题，智能体负责创建 GitHub issue。会在后台探索代码库以获取上下文和领域语言。当用户想要报告 bug、进行 QA、以对话方式提交 issue 或提到“QA 会话”时使用。
---

# QA 会话

运行一次交互式 QA 会话。用户描述他们遇到的问题。你进行澄清、探索代码库以获取上下文，并创建持久、以用户为中心、使用项目领域语言的 GitHub issue。

## 针对用户提出的每个 issue

### 1. 倾听并适度澄清

让用户用自己的话描述问题。最多问 **2-3 个简短的澄清问题**，聚焦：

- 他们期望发生什么 vs 实际发生了什么
- 复现步骤（如果不明显）
- 问题是稳定出现还是间歇出现

不要过度追问。如果描述已足够清晰，可以继续下一步。

### 2. 在后台探索代码库

与用户交谈的同时，启动一个 Agent（subagent_type=Explore）在后台了解相关区域。目标不是找到修复方案，而是：

- 了解该区域使用的领域语言（检查 UBIQUITOUS_LANGUAGE.md）
- 理解该功能应该做什么
- 识别面向用户的行为边界

这些上下文能帮你写出更好的 issue——但 issue 本身不应引用具体文件、行号或内部实现细节。

### 3. 评估范围：单个 issue 还是拆分？

在提交前，判断这是一个**单个 issue**，还是需要**拆分为多个 issue**。

需要拆分的情况：

- 修复跨越多个独立区域（例如“表单验证错误 AND 成功消息缺失 AND 重定向损坏”）
- 存在明显可分离的关注点，不同人可以并行处理
- 用户描述的内容包含多个不同的失败模式或症状

保持为单个 issue 的情况：

- 是一个地方的一个行为出错
- 所有症状都由同一个根因行为引起

### 4. 创建 GitHub issue(s)

使用 `gh issue create` 创建 issue。不要先让用户审阅——直接创建并分享 URL。

issue 必须是**持久的**——即使在重大重构后仍应可读。从用户视角撰写。

#### 单个 issue

使用此模板：

```
## What happened

[Describe the actual behavior the user experienced, in plain language]

## What I expected

[Describe the expected behavior]

## Steps to reproduce

1. [Concrete, numbered steps a developer can follow]
2. [Use domain terms from the codebase, not internal module names]
3. [Include relevant inputs, flags, or configuration]

## Additional context

[Any extra observations from the user or from codebase exploration that help frame the issue — e.g. "this only happens when using the Docker layer, not the filesystem layer" — use domain language but don't cite files]
```

#### 拆分（多个 issue）

按依赖顺序创建 issue（先创建阻塞项），以便引用真实的 issue 编号。

为每个子 issue 使用以下模板：

```
## Parent issue

#<parent-issue-number> (if you created a tracking issue) or "Reported during QA session"

## What's wrong

[Describe this specific behavior problem — just this slice, not the whole report]

## What I expected

[Expected behavior for this specific slice]

## Steps to reproduce

1. [Steps specific to THIS issue]

## Blocked by

- #<issue-number> (if this issue can't be fixed until another is resolved)

Or "None — can start immediately" if no blockers.

## Additional context

[Any extra observations relevant to this slice]
```

创建拆分时：

- **优先拆成多个小 issue，而不是少数大 issue** —— 每个都应能独立修复和验证
- **如实标注阻塞关系** —— 如果 issue B 确实要等 issue A 修复后才能测试，就明说。如果它们相互独立，就都标注为 "None — can start immediately"
- **按依赖顺序创建 issue**，以便在“Blocked by”中引用真实 issue 编号
- **最大化并行度** —— 目标是多个人（或智能体）能同时认领不同 issue

#### 所有 issue 正文的规则

- **不要包含文件路径或行号** —— 这些会很快过时
- **使用项目的领域语言**（如果存在，检查 UBIQUITOUS_LANGUAGE.md）
- **描述行为，而不是代码** —— “同步服务未能应用补丁”，而不是 “applyPatch() 在第 42 行抛出异常”
- **复现步骤必填** —— 如果无法确定，询问用户
- **保持简洁** —— 开发者应在 30 秒内读完 issue

创建完成后，打印所有 issue URL（并总结阻塞关系），然后问：“下一个 issue，还是结束？”

### 5. 继续会话

继续，直到用户说结束。每个 issue 相互独立——不要批量处理。
