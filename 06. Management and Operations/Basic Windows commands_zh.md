## 基本Windows命令

要确定当前的IPv6配置，请在Windows命令提示符下键入 `ipconfig /all`。

`ping` 和 `tracert` 在IPv6中都能正常工作。对于链路本地地址，Windows支持默认区域标识符（也称为默认接口），因此 `ping fe80::1234` 将自动使用默认接口。在具有多个网络接口的主机上，可以指定接口，例如 `ping fe80::1234%7`。正在使用的接口可以在 `ipconfig /all` 的输出中找到。

要检查基本的IPv6配置，请使用
`控制面板/所有控制面板项/网络和共享中心/更改适配器设置`。
选择感兴趣的网络适配器，然后选择 `属性/Internet协议版本6`，基本属性将可用。通常，不需要更改任何内容。

可以使用 `netsh` 从命令提示符检查或更改更高级的属性，例如，
`netsh interface ipv6 show privacy` 显示临时地址是否处于活动状态。
由于 `netsh` 是一个非常复杂的工具，我们在此不完全描述它，但它在每个级别都包含在线帮助，通过在命令中添加 `?` 即可，例如，`netsh interface ipv6 show interfaces ?`。

相同的功能（以及更多）也可以使用PowerShell使用，对此我们建议查阅Microsoft文档。


<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Packet%20size%20and%20Jumbo%20Frames.md) [<ins>下一页</ins>](../07.%20Case%20Studies/07.%20Case%20Studies.md) [<ins>返回顶部</ins>](06.%20Management%20and%20Operations.md)
