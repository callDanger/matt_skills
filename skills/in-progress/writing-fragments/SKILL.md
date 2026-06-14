---
name: writing-fragments
description: 一场 grilling 会话，从用户那里挖掘碎片——异质的写作小块（论断、片段、锋利句子、半成品想法）——并将它们追加到单一文档中，作为未来文章的原始素材。当用户想在施加结构之前先发展想法，或提到写作的 "fragments"、"ideate" 或 "raw material" 时使用。
---

<what-to-do>

运行一场生成碎片的 grilling 会话。围绕用户想写的任何内容，持续不断地采访他们。不要划分阶段、提纲或结构——这明确不在范围内。

当碎片从对话任意一方浮现时，将其追加到单一 markdown 文件中。用户会在会话期间编辑这个文件；因此写入前务必重新读取，以保留他们的修改。

如果用户没有传入路径，询问一次文档保存位置，然后在整个会话中记住它。

从用户说的第一句话开始就要捕捉碎片，包括最初的提示。

首次写入时，在顶部放一个 H1 工作标题（之后可以改），不要有其他内容——不要元数据、目录或日期。

</what-to-do>

<supporting-info>

## 什么是碎片

碎片是任何可能活到最终文章中的文本片段。它必须 _对作者可读_ ——作者能看懂它是什么意思——但不需要定义术语，也不需要让陌生读者完全理解。标准不是"这是一个自洽的论证吗？"，而是"这是一段好文字吗？"

碎片故意保持异质。以下是可能成为碎片的例子：

- 一句你想用在某处但还不知道放在哪里的锋利句子。
- 一个附带一行论证的论断。
- 一个片段：发生的一件事、一段代码、一个场景、一个类比。
- 一个半成品想法："关于 X 怎么感觉像 Y 的某种东西，以后再展开。"
- 一句引用、一段对话、一句无意间听到的话。
- 一组靠感觉聚在一起的、相关的观察。
- 一句抱怨、一个自白、一个 punchline。

小说家的日记就是模型：多年无结构的观察记录，之后被挖掘为原始素材。碎片就是观察记录。

## 文件格式

```markdown
# Working title

A first fragment lives here.

It can be multiple paragraphs. It can include lists, code, quotes — whatever
shape the fragment naturally takes.

---

A second fragment.

---

> A quoted line that the user wants to keep around.

A reaction to it.

---

- A cluster of related observations
- That hang together by feel
- And want to be near each other
```

碎片之间用水平线（`\n---\n`）分隔。正文内不使用标题。不加标签。除了添加顺序外，没有其他顺序。

## 写作节奏

静默追加。不要为每个碎片征求许可。顺带提一句你加了什么（"adding that"），但不要打断对话去弹保存对话框。

每次写入前：从磁盘重新读取文件。用户可能在回合之间编辑、重排或删除碎片——保留他们的更改。永远不要覆盖整个文件；只能追加（或者，如果用户要求，原地编辑某个特定碎片）。

用户可以随时说 "cut the last one"、"rewrite that one sharper"、"merge those two"。把这些当作一等指令处理。

</supporting-info>
