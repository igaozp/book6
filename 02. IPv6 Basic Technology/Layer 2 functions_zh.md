## 第2层功能

每个IPv6数据包都必须包装在第2层数据包（或帧）中，以便在"线路"上进行物理传输，在许多情况下，这当然更可能是光纤或无线电链路。这个陈述需要两个直接限定：

1. 对于具有非常小帧大小的硬件介质，IPv6数据包可能需要分割成几个第2层数据包。就IPv6而言，这*不是*分片，因为它作为第2层功能（有时称为"适配层"）处理，无论是硬件还是软件。

1. 对于IPv6-in-IPv4隧道，IPv4充当第2层；参见
   [3. 隧道](../03.%20Coexistence%20with%20Legacy%20IPv4/Tunnels.md)。

IPv6到以太网类链路（包括WiFi）的映射与到各种形式的无线网状网络的映射之间存在相当大的差异。以太网类链路（包括许多点对点链路）是一次发送或接收一个完整帧的链路，原始大小至少为1500字节，第2层有48位IEEE MAC地址。它必须提供或模拟经典的以太网多播。然后，IPv6映射遵循1998年的
[RFC 2464](https://www.rfc-editor.org/info/rfc2464)，除了
[RFC 6085](https://www.rfc-editor.org/info/rfc6085)中对多播地址细节的一些更新以及
[RFC 8064](https://www.rfc-editor.org/info/rfc8064)中对接口标识符的更新。IPv6有自己的以太网类型字段（0x86dd），因此可以在驱动程序级别区分IPv6和IPv4数据包。类似于RFC 2464的文档存在于其他几种硬件介质，通常称为"IPv6-over-foo"文档。

有趣的是，*没有*IPv6-over-WiFi文档；IPv6完全依赖于WiFi模拟以太网，包括多播。这对IPv6在WiFi上的可扩展性产生了影响，这在[RFC 9119](https://www.rfc-editor.org/info/rfc9119)中讨论。

以太网遗留帧大小为1500字节的结果是，IPv6的Internet范围要求的最小传输单元大小（MTU）设置为**1280字节**（从1500减少以允许可能的封装开销）。因此，*任何*IPv6-over-foo机制**必须**提供至少这个MTU，这适用于每个适配层。

IPv6可以通过PPP（点对点协议）链路传输
\[[RFC5072](https://www.rfc-editor.org/info/rfc5072)、
[RFC 5172](https://www.rfc-editor.org/info/rfc5172)\]。同样，它可以使用GRE（通用路由封装，
[RFC 7676](https://www.rfc-editor.org/info/rfc7676)）传输。

IPv6也可以通过MPLS基础设施传输
\[[RFC4029](https://www.rfc-editor.org/info/rfc4029)\]。更多细节可以在
\[[3. 隧道](../03.%20Coexistence%20with%20Legacy%20IPv4/Tunnels.md)\]中找到。

将IPv6映射到网状网络是相当不同的，网状网络没有对多播的本地支持，也没有像以太网那样的共享链路的简单模型。[RFC 9119](https://www.rfc-editor.org/info/rfc9119)在这里也是相关的，
[RFC 8376](https://www.rfc-editor.org/info/rfc8376)提供了所涉及挑战的一般背景。今天的运营经验有限，最佳实践尚未建立。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Addresses.md) [<ins>下一页</ins>](Address%20resolution.md) [<ins>顶部</ins>](02.%20IPv6%20Basic%20Technology.md)
