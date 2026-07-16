# book6/utilities 的 README

此目录包含一些不属于书籍本身但仍然有用的项目。

特别是这里有 [makeBook](./makeBook.py)，其作用是协调 book6 章节与目录，并尽可能设置章节间和小节间的链接。除非您知道自己在做什么，否则请不要运行它。同样，[indexBook](./indexBook.py) 更新索引（基于 [index6.txt](./index6.txt) 中的索引词），[RFCbib6.py](./RFCbib6.py) 重建 RFC 引用索引。

[bakeBook](./bakeBook.py) 将 book6 的所有章节"烘焙"成一个单一的 markdown 文件，用于生成书籍的 PDF 版本。

这些工具记录在 [utDoc.md](./utDoc.md) 中。
