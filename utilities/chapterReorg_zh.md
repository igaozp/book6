## 如何进行非标准更改

添加章节：

- 将纯文本章节名称添加到 Contents.md
  例如：```25. Interesting Stuff```
- 运行 makeBook

添加小节：

- 将名称添加到章节基础文件
  例如：```## Interesting Section```
- 运行 makeBook

删除小节：

- 删除小节文件
- 从章节基础文件中删除 ```##``` 行
- 运行 makeBook
- 运行 indexBook（并检查损坏引用的警告）

删除章节：

- 删除 ```N. Name directory```
- 从 Contents.md 中删除 ```N. Name``` 块
- 运行 makeBook
- 运行 indexBook（并检查损坏引用的警告）

重命名小节：

- 重命名小节文件
- 更改小节文件中的 ``##`` 文本
- 更改章节基础文件中的 ``##`` 链接
- 运行 makeBook
- 运行 indexBook（并检查损坏引用的警告）

重命名或重新编号章节：

- 在 Contents.md 中重命名章节
  例如：```11. Chapter Test```
- 重命名章节目录
- 重命名章节基础文件
- 更改基础文件中的标题
  例如：```# 11. Chapter Test```
- 运行 makeBook
- 运行 indexBook（并检查损坏引用的警告）
