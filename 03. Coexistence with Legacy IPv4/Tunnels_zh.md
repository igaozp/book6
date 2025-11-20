## 隧道

最简单的情况是，两个 IPv6 主机或网络可以通过隧道经由 IPv4 连接在一起，即每端的设备充当隧道端点的安排。通常，这样的隧道连接两个 IPv6 路由器，使用
[RFC 4213](https://www.rfc-editor.org/info/rfc4213) 中描述的非常简单的 IPv6-in-IPv4 封装，使用 IP 协议编号 41 告诉 IPv4 有效负载是 IPv6。相反，IPv4-in-IPv6 隧道也是可能的，使用 IPv6 下一个头部值 4 告诉 IPv6 有效负载是 IPv4。这将允许运营商通过 IPv6 骨干网互连两个 IPv4 孤岛。（当然，如果需要，IPv6-in-IPv6 隧道也是可能的。）

然而，今天很少需要这种简单的封装，因为主要 ISP 广泛提供直接 IPv6 传输。隧道用于其他共存场景，我们现在将描述其中一些。

早期的解决方案假设 ISP 的基础设施主要是 IPv4；
[RFC 6264](https://www.rfc-editor.org/info/rfc6264) 不再是最新的，但它提供了关于在这种情况下如何使用 IPv6-in-IPv4 隧道的背景。今天，情况相反，重点是主要是 IPv6 的 ISP 基础设施。

DS-Lite（IPv4 耗尽后的双栈精简版宽带部署）\[[RFC6333](https://www.rfc-editor.org/info/rfc6333)\] 在 ISP 的运营商级 NAT (CGN) 和客户的客户边缘 (CE) 路由器之间使用 IPv4-in-IPv6 隧道。客户被给予私有 IPv4 前缀
\[[RFC1918](https://www.rfc-editor.org/info/rfc1918)\]，CGN 将 IPv4 流量转换为公共 IPv4 地址或从公共 IPv4 地址转换。因此，CGN 和 CE 路由器之间的基础设施可以是纯 IPv6。

IPv6 可以使用 GRE（通用路由封装，
[RFC 7676](https://www.rfc-editor.org/info/rfc7676)）进行隧道传输。

IPv6 可以使用 6rd
\[[RFC5969](https://www.rfc-editor.org/info/rfc5969)\] 通过纯 IPv4 ISP 基础设施承载（但请参阅
\[[过时的技术](Obsolete%20techniques.md)\]）。

IPv6 可以通过 MPLS 隧道传输
\[[RFC4029](https://www.rfc-editor.org/info/rfc4029)\]；例如，参见"使用 IPv6 提供商边缘路由器 (6PE) 通过 IPv4 MPLS 连接 IPv6 孤岛"
\[[RFC4798](https://www.rfc-editor.org/info/rfc4798)\]。一个常见的解决方案是通过 IPv6 提供商边缘路由器 (6PE) 通过 IPv4 MPLS 连接 IPv6 网络
\[[RFC4798](https://www.rfc-editor.org/info/rfc4798)\]。
[RFC 7439](https://www.rfc-editor.org/info/rfc7439) 为纯 IPv6 MPLS 网络提供了差距分析。
[RFC 7552](https://www.rfc-editor.org/info/rfc7552) 弥补了许多这些差距。感兴趣的读者可以学习一个 125 页的
[NANOG 教程](https://pc.nanog.org/static/published/meetings/NANOG76/1993/20190612_Agahian_Demystifying_Ipv6_Over_v1.pdf)。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Dual%20stack%20scenarios.md) [<ins>下一页</ins>](Translation%20and%20IPv4%20as%20a%20service.md) [<ins>顶部</ins>](03.%20Coexistence%20with%20Legacy%20IPv4.md)
