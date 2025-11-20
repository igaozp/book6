## 流量类和流标签

每个IPv6数据包中的流量类是一个字节，也称为差异化服务字段。它在每个方面都被完全视为每个IPv4数据包中的相同字段（最初在[RFC 791](https://www.rfc-editor.org/info/rfc791)中命名为TOS八位字节）。它包含六位
[差异化服务](https://www.rfc-editor.org/info/rfc2474)代码点，后跟两个
[ECN（显式拥塞通知）](https://www.rfc-editor.org/info/rfc3168)位。[RFC 8100](https://www.rfc-editor.org/info/rfc8100)对ISP的当前差异化服务互连实践提供了良好的概述。[RFC 5127](https://www.rfc-editor.org/info/rfc5127)、
[RFC 4594](https://www.rfc-editor.org/info/rfc4594)、
[RFC 5865](https://www.rfc-editor.org/info/rfc5865)、
[RFC 8622](https://www.rfc-editor.org/info/rfc8622)和
[RFC 8837](https://www.rfc-editor.org/info/rfc8837)也描述了当前的实践。

ECN旨在供传输协议用于支持拥塞控制。

流标签是每个IPv6数据包中的20位字段，尽管如其名称所示，它仅与持续的流量流相关。数据包的发送者应该用给定流量流（例如给定的TCP连接）唯一的伪随机非零值填充它。然后它可以在下游用于支持负载均衡。根据定义，这20位没有语义，尽管已知一些部署违反了此指南，这将干扰负载均衡。参见
[IPv6流标签规范](https://www.rfc-editor.org/info/rfc6437)、
[在隧道中使用IPv6流标签进行等成本多路径路由和链路聚合](https://www.rfc-editor.org/info/rfc6438)
和
[在服务器场中使用IPv6流标签进行负载均衡](https://www.rfc-editor.org/info/rfc7098)。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Extension%20headers%20and%20options.md) [<ins>下一页</ins>](Source%20and%20Destination%20Address%20Selection.md) [<ins>顶部</ins>](02.%20IPv6%20Basic%20Technology.md)
