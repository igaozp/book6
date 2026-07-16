## 双栈场景

我们必须区分原始的双栈部署模型和在 IPv6 基础设施上提供 IPv4 作为*服务*的同时向上层协议呈现双栈的新概念。

### 原始双栈模型

双栈最初在 [RFC 4213](https://www.rfc-editor.org/rfc/rfc4213) 中描述（连同基本隧道技术）。在 2020 年，它似乎是部署最广泛的 IPv6 解决方案（约 50%，参见
[ETSI-IP6-WhitePaper](https://www.etsi.org/images/files/ETSIWhitePapers/etsi_WP35_IPv6_Best_Practices_Benefits_Transition_Challenges_and_the_Way_Forward.pdf) 中报告的统计数据）。

在经典的双栈部署中，链路上的数据包要么是原生 IPv6，要么是原生 IPv4。所有路由器同时支持 IPv6 和 IPv4，具有独立的路由表：这被称为"擦肩而过的船"。

```
Ships that pass in the night, and speak [to] each other in passing,
only a signal shown, and a distant voice in the darkness
  --  Henry Wadsworth Longfellow, 1863
```

今天，互联网的核心——所有主要的国际传输提供商和所有主要的互联网交换点——都支持双栈路由。许多本地 ISP 也是如此。

此外，双栈网络中的所有主机都应该同时支持 IPv6 和 IPv4，并优先使用 IPv6。这种部署可以容忍传统的纯 IPv4 主机和应用程序的存在，并且可以无需特殊安排即可访问外部的纯 IPv4 服务。该模型的一个重要部分是，使用网络的应用程序看到的是本质上同时支持 IPv4 和 IPv6 的套接字 API 版本。因此，
\[[RFC3542](https://www.rfc-editor.org/info/rfc3542)\] 引入了双栈 API，包括重要的 `getaddrinfo()`（"获取地址信息"）函数，该函数自那时起被 POSIX 和 Windows 操作系统采用。

[RFC 8305](https://www.rfc-editor.org/info/rfc8305) 解释了应用程序寻求优化双栈性能的"Happy Eyeballs"技术。

通过双栈，IPv6 可以与其他网络升级一起引入，网络管理和信息技术 (IT) 系统的许多部分仍然可以在 IPv4 中工作。事实上，IPv4 可达性可以提供很长时间，大多数互联网服务提供商 (ISP) 正在利用运营商级 NAT（CGN，
[RFC 6888](https://www.rfc-editor.org/info/rfc6888)）来延长 IPv4 的寿命。然而，大型 ISP 已经发现了 CGN 的扩展限制和运营成本。

这种经典双栈方法的一个缺口是它不允许纯 IPv6 客户端与纯 IPv4 服务器通信。纯 IPv6 设备确实存在，例如
[Thread](https://www.threadgroup.org/What-is-Thread/Overview) 设备，预计未来会有更多。这种情况需要转换机制，例如 NAT64 + DNS64（参见
\[[转换和 IPv4 即服务](Translation%20and%20IPv4%20as%20a%20service.md)\]），这将允许双栈网络上的纯 IPv6 设备访问 IPv4 主机。通常，同一网络上的双栈客户端也将使用 NAT64（而不是
[RFC 1918](https://www.rfc-editor.org/info/rfc1918) 地址和 NAT44）来访问纯 IPv4 主机，但它们无论如何都在使用 NAT。参见这篇有用的
[博客文章](https://sgryphon.gamertheory.net/2022/12/14/running-nat64-in-a-dual-stack-network/)。

一个具体的问题是，如果不提供 IPv6/IPv4 共存，SIP（IP 电话的会话发起协议）将无法工作
\[[RFC6157](https://www.rfc-editor.org/info/rfc6157)\]。

虽然双栈在部署的初始阶段提供了优势，但从长远来看它有一些缺点，例如网络资源和状态的重复。它还需要更多的 IPv4 地址，从而增加资本支出 (CAPEX) 和运营支出 (OPEX)。需要明确的是，今天的网络（无论是家庭网络还是办公网络）可以非常顺畅地工作，每个主机都有 IPv4 地址和 IPv6 地址，并使用对特定应用程序效果最好的那个。

### IPv6-Mostly 网络

随着 [RFC 8925](https://www.rfc-editor.org/info/rfc8925)（"DHCPv4 的 IPv6-Only Preferred 选项"）的标准化，现在存在一种可支持的标准机制，可以优雅地从传统 IP 迁移出去，同时为不支持 IPv6 或仅支持经典双栈的系统和网络栈保留访问权限。（此类系统不会自动支持下面描述的 464XLAT 技术，或由于应用程序或内部操作系统要求而无法在没有传统 IPv4 的情况下运行）。IPv6-mostly 提供的是一种低风险模式，以非常渐进的方式将传统 IPv4 或现有双栈网络转换为纯 IPv6。通过利用传统 IPv4 的 IPv6-only-preferred 选项（DHCP 选项 108），运营商能够通过可能已经在使用的网络协议（用于 IPv4 的 DHCP）发出信号，表明如果主机能够利用它们，网络能够支持纯 IPv6 机制。相反，如果设备没有实现和理解 DHCP 选项 108，它们会愉快地继续使用双栈 IPv4/IPv6 体验，同样无需用户干预。

这种方法具有几个优势，特别是简化网络段和协议部署。这种部署模型允许主机栈"以其最高的演化水平运行"，只要它们能够，并且基于来自 DHCP 服务器的信号，在 DHCP 事务中通信的持续时间内禁用其传统 IP 栈。这种"定时禁用"方法还允许进行测量测试，如果需要短时间测试禁用传统 IPv4，并保证它将被重新启用。此外，这允许运营商以其运营领域内操作系统演化的速度缓慢地从传统 IPv4 迁移出去，并允许在给定网络段上多种主机的共存：纯 IPv4 主机、纯 IPv6 主机和双栈主机。随着操作系统添加对 DHCP 选项 108 的支持，对传统 IPv4 的依赖自然会变得越来越小，直到最终可以禁用它或减少到足以删除它的程度。

在这种情况下观察到一个操作故障。如果支持 DHCP 选项 108 的主机有任何类型的错误配置导致 IPv6 无法正常工作，它可能会进入一种状态，即它禁用 IPv4 但也没有 IPv6 连接。例如，如果主机的内在防火墙配置为阻止传入的 ICMPv6 和 IPv6 数据包，但主机遵守选项 108，当它遇到 IPv6-mostly 网络时，它将无法连接到任何一个版本的 IP。这种错误配置已经在具有强制性企业安全配置的笔记本电脑中观察到，当它们漫游到企业网络之外的 IPv6-mostly 网络时。

除了这个问题之外，通过 IPv6-mostly 进行受控和有意的迁移允许操作系统决定它能支持多少或多少，而无需用户的输入，使网络适应主机的能力，从而降低不兼容的风险（并降低问题报告的率）。与大多数现有的纯 IPv6 网络一样，IPv6-mostly 仍然需要数据包和 DNS 转换服务
（[稍后讨论](Translation%20and%20IPv4%20as%20a%20service.md)）以及用于转换的 IPv6 前缀的知识
（[同上](Translation%20and%20IPv4%20as%20a%20service.md)）。通过支持这些功能，IPv6-mostly 网络上的主机将拥有完整的功能套件。

这里有一份关于 IPv6-mostly 的优秀部署报告
[在一个大型会议上](https://nsrc.org/blog/apricot-ipv6-only)。

### IPv4 即服务的需求

全球唯一的 IPv4 地址现在稀缺并具有重要的商业价值。实际上，即使使用 CGN 的私有 IPv4 地址，CGN 系统的全局 IPv4 地址也必须由某人支付。

因此，当 IPv6 使用超过某个阈值时，开始向下一阶段过渡并转向更高级的 IPv6 部署（也称为纯 IPv6）可能是有利的。需要明确的是，这并不意味着删除对纯 IPv4 资源的访问。必须保留某种访问 IPv4 资源的方法，因为主要网络基础设施从双栈切换。实际上，主机中的*应用层*仍然会看到双栈环境，即使链路上的数据包不再是原生 IPv6 和原生 IPv4 的混合。

此类解决方案被称为"IPv4 即服务"(IPv4aaS)，可用于在开始基础设施的纯 IPv6 过渡时确保 IPv4 支持和共存。这可能是一个复杂的决定。如 [RFC 9386](https://www.rfc-editor.org/info/rfc9386) 中所述，纯 IPv6 通常与范围相关联，例如纯 IPv6 覆盖或纯 IPv6 底层。

"纯 IPv6 覆盖"表示网络域的端点之间的覆盖隧道仅基于 IPv6。固定网络中的纯 IPv6 覆盖意味着 IPv4 至少在提供商边缘 (PE) 节点和客户边缘 (CE) 节点（或宽带网络网关 (BNG)）的接口之间封装在 IPv6 中（或转换）。如 [隧道](Tunnels.md) 中进一步提到的，隧道提供了一种使用现有 IPv4 基础设施来承载 IPv6 流量的方法。还有
[转换和 IPv4 即服务](Translation%20and%20IPv4%20as%20a%20service.md) 中描述的转换选项。这种采用纯 IPv6 覆盖的方法有助于保持与现有 IPv4 基础的兼容性，但它不是一个长期解决方案

"纯 IPv6 底层"与特定域相关，例如纯 IPv6 接入网络或纯 IPv6 骨干网，意味着 IPv6 是所有流量传输的网络协议。控制平面和数据平面都是基于 IPv6 的。例如，固定网络中的纯 IPv6 底层意味着底层网络协议在任何提供商边缘 (PE) 节点之间仅为 IPv6。

为了确保 IPv4 支持，引入了 IPv4aaS 的概念，意味着 IPv4 连接是通过共存机制提供的，因此存在封装/转换 + 纯 IPv6 底层 + 解封装/转换的组合。IPv4aaS 为用户提供双栈服务，并允许 ISP 在网络中运行纯 IPv6，通常是接入网络。一些网络运营商已经开始了这个过程，例如
[T-Mobile US](https://pc.nanog.org/static/published/meetings/NANOG73/1645/20180625_Lagerholm_T-Mobile_S_Journey_To_v1.pdf)、
[Reliance Jio](https://datatracker.ietf.org/meeting/109/materials/slides-109-v6ops-ipv6-only-adoption-challenges-and-standardization-requirements-03)
和
[EE](https://indico.uknof.org.uk/event/38/contributions/489/attachments/612/736/Nick_Heatley_EE_IPv6_UKNOF_20170119.pdf)。

[RFC 9313](https://www.rfc-editor.org/info/rfc9313) 比较了最常见的 IPv6 过渡解决方案的优点，即 464XLAT
\[[RFC6877](https://www.rfc-editor.org/info/rfc6877)\]、DS-lite
\[[RFC6333](https://www.rfc-editor.org/info/rfc6333)\]、Lightweight 4over6 (lw4o6) \[[RFC7596](https://www.rfc-editor.org/info/rfc7596)\]、MAP-E \[[RFC7597](https://www.rfc-editor.org/info/rfc7597)\] 和 MAP-T
\[[RFC7599](https://www.rfc-editor.org/infoc/rfc7599)\]。

当前草案中提出了运营商的框架
\[[draft-ietf-v6ops-framework-md-ipv6only-underlay](https://datatracker.ietf.org/doc/draft-ietf-v6ops-framework-md-ipv6only-underlay/)\]。
客户边缘路由器需要支持
[RFC 8585](https://www.rfc-editor.org/info/rfc8585)。读者会注意到，今天最常采用的解决方案，例如这个，利用了隧道（通过 IPv6 承载 IPv4）和转换（IPv4 重新编码为 IPv6）的使用。以下两节分离出这两种技术。
\[[3. 转换](../03.%20Coexistence%20with%20Legacy%20IPv4/Translation%20and%20IPv4%20as%20a%20service.md)\]
还提供了有关 IPv4aaS 的更多详细信息。

<!-- Link lines generated automatically; do not delete -->

### [<ins>下一页</ins>](Tunnels.md) [<ins>顶部</ins>](03.%20Coexistence%20with%20Legacy%20IPv4.md)
