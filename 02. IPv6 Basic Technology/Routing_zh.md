## 路由

本节是对复杂主题的简短介绍。IPv6数据包像任何数据报协议一样单独且无状态地路由。连续的数据包可能遵循不同的路由，可能在途中丢失，可能乱序到达，传输时间是可变的。在实践中，运营商试图最小化这些影响，但上层协议不能依赖于此。在某些情况下，服务质量机制，例如差异化服务
\[[2. 流量类和流标签](../02.%20IPv6%20Basic%20Technology/Traffic%20class%20and%20flow%20label.md)\]
可能有所帮助，但数据包传递仍然是统计性的。

IPv6路由通常通过最长匹配运行，即每个路由器将每个数据包转发到已知处理与数据包的目标地址匹配的最长地址前缀（最多128位）的另一个路由器
\[[BCP198](https://www.rfc-editor.org/info/bcp198)\]。路由器之间使用各种路由协议来分发关于它们处理哪些前缀的信息。常见的路由协议是：

*对于站点和企业网络：*

- OSPFv3 \[[RFC5340](https://www.rfc-editor.org/info/rfc5340)\]最常见。

- IS-IS \[[RFC5308](https://www.rfc-editor.org/info/rfc5308)、
  [RFC 7775](https://www.rfc-editor.org/info/rfc7775)\]。

- RIPng \[[RFC2080](https://www.rfc-editor.org/info/rfc2080)、
  [RFC 2081](https://www.rfc-editor.org/info/rfc2081)\]已定义，但似乎很少使用。

*小型企业和家庭网络*

- Babel路由协议
  \[[RFC8966](https://www.rfc-editor.org/info/rfc8966)\]。

*在运营商（ISP）网络或非常大的企业网络内部：*

- IBGP（BGP-4的内部使用）通过路由反射优化
  \[[RFC4456](https://www.rfc-editor.org/info/rfc4456)\]。

- IS-IS \[[RFC5308](https://www.rfc-editor.org/info/rfc5308)、
  [RFC 7775](https://www.rfc-editor.org/info/rfc7775)\]

- OSPFv3 \[[RFC5340](https://www.rfc-editor.org/info/rfc5340)\]。

*在运营商（ISP）网络之间（域间路由）：*

- 边界网关协议4（BGP-4）的多协议形式
  \[[RFC2545](https://www.rfc-editor.org/info/rfc2545)、
  [RFC 4271](https://www.rfc-editor.org/info/rfc4271)、
  [RFC 4760](https://www.rfc-editor.org/info/rfc4760)\]。自治系统号对IPv6和IPv4的工作方式相同。

*对于新兴的网状网络：*

- RPL（用于低功耗和有损网络的IPv6路由协议）
  \[[RFC6550](https://www.rfc-editor.org/info/rfc6550)、
  [RFC 9008](https://www.rfc-editor.org/info/rfc9008)、
  [RFC 9010](https://www.rfc-editor.org/info/rfc9010)\]。

- Babel路由协议
  \[[RFC8966](https://www.rfc-editor.org/info/rfc8966)\]。

IPv6路由器可以分为各种类别，每个类别都需要激活不同的功能。这些类别可能重叠：

- 客户边缘（CE）路由器（企业）：这些是将企业网络连接到一个或多个ISP的路由器
  \[[RFC7084](https://www.rfc-editor.org/info/rfc7084)、
  [RFC 8585](https://www.rfc-editor.org/info/rfc8585)、
  [RFC 9096](https://www.rfc-editor.org/info/rfc9096)\]。

- 企业路由器：大型企业网络内的内部路由器。

- 子网路由器：支持连接终端主机（通常是以太网或WiFi）的一个或多个链路的内部路由器。这样的路由器将是传入流量的最后一跳路由器和传出流量的第一跳路由器。它还必须为终端主机提供路由器通告服务，以及SLAAC或DHCPv6或两者\[参见
  [2. 地址解析](../02.%20IPv6%20Basic%20Technology/Address%20resolution.md)
  等\]。

- 客户边缘（CE）路由器（家庭）：这些是将家庭或小型办公室网络连接到ISP的廉价路由器。它们通常也充当子网路由器，但不太可能提供完整的企业CE路由器服务集。它们需要很少或不需要配置即可进行基本操作。

- 提供商边缘路由器。这些是ISP网络内直接连接到CE路由器的路由器。

- ISP内的传输路由器。

- 将ISP连接到对等ISP和/或互联网交换点的域间路由器。

一个一般性评论是，IPv6前缀比IPv4前缀长（最多64位而不是，比如说，24位），人们可能期望路由表需要更多的内存空间。虽然这是真的，但IPv6从一开始就被设计为无类路由聚合，这通常允许有更少的IPv6前缀，缓解了表大小问题。（尽管如此，IPv6的BGP-4表继续增长，如
[这篇CCR论文](https://dl.acm.org/doi/10.1145/3477482.3477490)中所讨论的。）感兴趣的读者可以在
[Geoff Huston的网站](https://bgp.potaroo.net/index-bgp.html)上找到关于BGP-4表大小的详尽数据。有关BGP-4本身的深入探讨，重点关注IPv6，请参阅Iljitsch van Beijnum的电子书：
[使用BGP进行互联网路由](https://www.iljitsch.com/2022/11-18-new-e-book-internet-routing-with-bgp.html)
（2022年）。

如
[3. 双栈场景](../03.%20Coexistence%20with%20Legacy%20IPv4/Dual%20stack%20scenarios.md)中所解释的，
IPv6路由通常独立于IPv4路由工作，这确实是一个基本的设计选择。但是，如果需要，封装的IPv4流量可以通过仅IPv6路径传输。为实现这一点，多协议BGP-4具有通过仅IPv6路径通告IPv4可达性的规定
\[[RFC8950](https://www.rfc-editor.org/info/rfc8950)\]。

最后，IPv6允许路由头，由数据包路径上的中间节点解释。这些在
[扩展头和选项](Extension%20headers%20and%20options.md)中简要解释。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](DNS.md) [<ins>下一页</ins>](Transport%20protocols.md) [<ins>顶部</ins>](02.%20IPv6%20Basic%20Technology.md)
