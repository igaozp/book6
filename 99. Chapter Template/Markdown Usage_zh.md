## Markdown 使用

使用 GitHub 方言的 markdown 的基础知识[在这里](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)。作为一般规则，请使用更简单的构造并避免花哨的格式。

不要忘记，本书任何章节中的每个新小节都需要一个单独的 .md 文件。

对于某些 markdown 编辑工具，没有换行的流式文本是一个麻烦。最好在约 72 个字符处换行。makeBook 将在需要将文件写回时使用 `mdformat` 工具执行此操作。

网页引用可以采用基本 markdown 形式，即：

```
  [text](URL)               引用任何有效的 URL
```

但也可以使用从 kramdown 改编的功能，例如

```
  {{RFC8200}}               引用 RFC
  {{BCP198}}                引用 IETF 最佳当前实践
  {{STD86}}                 引用 IETF 互联网标准
  {{I-D.ietf-v6ops-xxx}}    引用互联网草案
  {{draft-ietf-v6ops-xxx}}  同样！
  {{Last Section}}          引用当前章节中的小节
  {{2. Addresses}}          引用另一章节中的小节（需要单个空格）
```

这些引用将在下次运行 makeBook 时修复，因为 GitHub 的内置 markdown 不识别它们。对 RFC、草案名称等有一些检查（但仅当 makeBook 可以访问网络时）。

*注 1：*引用将用方括号括起来，如：\[[RFC8200](https://www.rfc-editor.org/info/rfc8200)\]。如果您出于语法原因不想使用方括号，例如使用 [RFC 8200](https://www.rfc-editor.org/info/rfc8200) 作为名词，请使用*三个*大括号：

```
  {{{RFC8200}}}
  {{{2. Addresses}}}
```

*注 2：*如果您将多个引用串在一起，例如，

```
  {{RFC4291}}{{RFC8200}}
```

它们将显示在带有逗号的单对方括号中：\[[RFC4291](https://www.rfc-editor.org/info/rfc4291), [RFC 8200](https://www.rfc-editor.org/info/rfc8200)\]。

*注 3：*如果您需要引用 RFC 的特定小节*并且*您知道相应的哈希标签，则可以使用此格式：

```
  Section 2.5.6 of {{{RFC3513#section-2.5.6}}}
```

但是，makeBook 无法以算法方式创建或检查哈希标签，因此您必须确保它是正确的。

图表可以是 ASCII 艺术（如果适用），在前后使用 `~~~`，例如：

```
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |Version| Traffic Class |           Flow Label                  |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |         Payload Length        |  Next Header  |   Hop Limit   |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                              etc.                             |
```

更复杂的图表可以使用单独的绘图工具（如 [*mermaid*](https://mermaid.live) 或 [*dia*](http://dia-installer.de/)）生成的 PNG 包含，PNG 文件也存储在 GitHub 上，例如：

*mermaid* 图表的来源：

````
```mermaid
flowchart LR
    S[Start here] --> E[End here]
```
````

作为由 [*mermaid.live*](https://mermaid.live) 生成的 PNG 文件嵌入到 markdown 中：

```
<img src="./example1.png" width=250 alt="Start here, end here">
```

如此显示：

<img src="./example1.png" width=250 alt="Start here, end here">

使用 *dia* 生成的示例：

```
<img src="./diag.png" alt="Disk feeding tape">
```

<img src="./diag.png" alt="Disk feeding tape">

请添加替代文本以帮助有视觉困难的人。

*注 4：*不建议在 markdown 源代码中直接使用 *mermaid*，因为这会在生成 book6 的 PDF 版本时造成困难。

*注 5：*本节的早期版本推荐使用 SVG 格式。这已被删除，因为 SVG 在生成 book6 的 PDF 版本时会造成困难。

可以以相同的方式插入 JPG 格式的现有图表。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Section%20Template.md) [<ins>下一页</ins>](Last%20Section.md) [<ins>返回顶部</ins>](99.%20Chapter%20Template.md)
