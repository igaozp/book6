此文件夹 `pdf` 用于生成 book6 的完整 PDF 文件，除此之外没有其他用途。

此文件夹的内容是进行中的工作，不面向读者。
公开的 PDF 版本托管在 https://ipv6textbook.com/。

图像文件在此处有意重复。

中间文件 `baked.md` 是整本书的完整 markdown 文件，由 `bakeBook.py` 工具制作。该工具还尝试首先将 `baked.md` 转换为 LaTeX 文件 `baked.tex`，然后转换为 PDF 文件 `baked.pdf`。如果失败，请尝试以下手动过程。

首先使用 pandoc 转换为 LaTeX：

```
pandoc baked.md -f gfm -t latex -s -o baked.tex -V colorlinks=true
```

然后是棘手的部分。_手动编辑_ `baked.tex`（使用任何文本编辑器），将所有出现的 `backslashpagebreak` 更改为 `\pagebreak`。
在 Linux 中，您可以在 `baked.tex` 所在的目录中简单地使用 `sed -i 's|^backslashpagebreak$|\\pagebreak|g' baked.tex`

然后将 LaTeX 文件转换为 PDF。在 Windows 上使用 `TeXworks` 或命令 `pdflatex baked.tex` 可以获得良好结果（后者需要运行两次以满足引用）。
