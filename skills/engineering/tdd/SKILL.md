---
name: tdd
description: 通过红-绿-重构循环进行测试驱动开发。当用户希望使用 TDD 构建功能或修复缺陷、提到"红-绿-重构"、希望编写集成测试，或要求进行测试先行开发时使用。
---

# 测试驱动开发

## 理念

**核心原则**：测试应通过公共接口验证行为，而非实现细节。代码可以完全改变；测试不应随之改变。

**好的测试**采用集成测试风格：它们通过公共 API 执行真实代码路径。它们描述 _系统做什么_，而不是 _怎么做_。一个好的测试读起来像一份规格说明——"用户可以使用有效购物车结账"准确地告诉你存在什么能力。这类测试在重构中能够存活，因为它们不关心内部结构。

**坏的测试**与实现紧耦合。它们 mock 内部协作者、测试私有方法，或通过外部手段验证（例如直接查询数据库而不是使用接口）。警告信号是：当你重构时测试失败了，但行为并没有改变。如果你重命名了一个内部函数而测试失败，那些测试就是在测试实现，而不是行为。

参见 [tests.md](tests.md) 了解示例，以及 [mocking.md](mocking.md) 了解 mock 指南。

## 反模式：水平切片

**不要先写所有测试，再写所有实现。** 这是"水平切片"——把 RED 阶段当作"写所有测试"，把 GREEN 阶段当作"写所有代码"。

这会产生**糟糕的测试**：

- 批量编写的测试验证的是想象出来的行为，而非实际行为
- 你最终测试的是事物的形态（数据结构、函数签名），而不是用户可感知的行为
- 测试对真实变化变得不敏感——行为破坏时通过，行为正常时失败
- 你超出了自己的视野，在尚未理解实现之前就确定了测试结构

**正确方法**：通过 tracer bullet 进行垂直切片。一个测试 → 一个实现 → 重复。每个测试都回应当前周期所学到的内容。因为你刚刚写好了代码，所以你清楚地知道什么行为重要以及如何验证它。

```
WRONG (horizontal):
  RED:   test1, test2, test3, test4, test5
  GREEN: impl1, impl2, impl3, impl4, impl5

RIGHT (vertical):
  RED→GREEN: test1→impl1
  RED→GREEN: test2→impl2
  RED→GREEN: test3→impl3
  ...
```

## 工作流程

### 1. 规划

探索代码库时，使用项目的领域词汇表，使测试名称和接口术语与项目语言保持一致，并尊重你所涉及领域的 ADR。

编写任何代码之前：

- [ ] 与用户确认需要哪些接口变更
- [ ] 与用户确认要测试哪些行为（按优先级排序）
- [ ] 识别 [deep modules](deep-modules.md) 的机会（小接口、深实现）
- [ ] 为[可测试性](interface-design.md)设计接口
- [ ] 列出要测试的行为（而非实现步骤）
- [ ] 获得用户对计划的批准

提问："公共接口应该是什么样的？哪些行为最重要，值得测试？"

**你无法测试所有内容。** 与用户确认哪些行为最重要。将测试精力集中在关键路径和复杂逻辑上，而不是每一个可能的边界情况。

### 2. Tracer Bullet

编写一个测试，验证系统的一个行为：

```
RED:   Write test for first behavior → test fails
GREEN: Write minimal code to pass → test passes
```

这是你验证端到端路径是否可行的 tracer bullet。

### 3. 增量循环

对于每个剩余行为：

```
RED:   Write next test → fails
GREEN: Minimal code to pass → passes
```

规则：

- 一次只写一个测试
- 只写足够让当前测试通过的代码
- 不要预判未来的测试
- 让测试聚焦于可观察的行为

### 4. 重构

所有测试通过后，寻找[重构候选](refactoring.md)：

- [ ] 消除重复
- [ ] 深化模块（将复杂度隐藏到简单接口之后）
- [ ] 在合适的地方应用 SOLID 原则
- [ ] 思考新代码对现有代码的启示
- [ ] 每次重构步骤后都运行测试

**不要在 RED 阶段重构。** 先到达 GREEN。

## 每个周期的检查清单

```
[ ] Test describes behavior, not implementation
[ ] Test uses public interface only
[ ] Test would survive internal refactor
[ ] Code is minimal for this test
[ ] No speculative features added
```
