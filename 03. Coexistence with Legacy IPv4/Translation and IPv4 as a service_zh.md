## 转换和 IPv4 即服务

当运营商希望通过运行单一协议 IPv6 而不是双栈来降低基础设施成本时，战略方法是最小化网络中的 IPv4 存在。不幸的是，某些资源仅在 IPv4 上可用，某些客户端应用程序可能*需要* IPv4。因此，在可预见的未来，纯 IPv6 环境是不现实的。在某些情况下，隧道（如上所述）就足够了，但通常 IPv6 和 IPv4 之间的转换是不可避免的。特别是，在提供 IPv4 即服务 (IPv4aaS) 时，典型的场景将：

1. 让 IPv6 原生流量在客户端和服务器之间直接流动。
1. 使用集中式 NAT64 设备将本地 IPv6 客户端的流量转换为远程纯 IPv4 服务器。
1. 在客户端上将字面 IPv4 地址请求封装到 IPv6 中，然后在集中式 NAT 上解封装并转换它以访问 IPv4 服务器。

因此，将转换技术的讨论与 IPv4 即服务的讨论分开实际上是不可能的。

### 术语

- SIIT（无状态 IP/ICMP 转换算法）。这也简称为"IP/ICMP 转换算法"
  \[[RFC7915](https://www.rfc-editor.org/info/rfc7915)、
  [RFC 6144](https://www.rfc-editor.org/info/rfc6144)\]。它将 IPv4 数据包转换为 IPv6 格式，反之亦然。请注意，转换仅限于基本功能，并且不转换任何 IPv4 选项或除分片头之外的任何 IPv6 扩展头。从技术上讲，该机制是无状态的（即，它不依赖于存储的信息），但实际上它被用作有状态机制的一部分。

- NAT64 指的是使用 SIIT 机制在 IPv6 客户端和 IPv4 服务器之间进行地址转换。

  - [RFC 6146](https://www.rfc-editor.org/info/rfc6146) 定义了_有状态_ NAT64，它（像 IPv4 NAT 一样）包括端口转换并支持双向传输会话。
  - DNS64 \[[RFC6147](https://www.rfc-editor.org/info/rfc6147)\]
    支持有状态 NAT64 客户端的 DNS 扩展。
  - PREF64 指的是在 NAT64 转换器"外部"使用的 IPv6 前缀。[RFC 8781](https://www.rfc-editor.org/info/rfc8781) 和
    [RFC 8880](https://www.rfc-editor.org/info/rfc8880) 是主机可以学习正在使用的 PREF64 的机制。
    [RFC 9872](https://www.rfc-editor.org/info/rfc9872) 建议所有运营商支持 RFC 8781，即如果可能，通过路由器通告宣布 PREF64。

- 464XLAT（有状态和无状态转换的组合）
  \[[RFC6877](https://www.rfc-editor.org/info/rfc6877)\] 是 SIIT 加上地址转换*从* IPv4 客户端到 IPv6 传输和*回到* IPv4 服务器。这用于 IPv4 流量穿越纯 IPv6 网络。

  - CLAT 是 464XLAT 中的客户端转换器。它实现无状态 NAT46 (SIIT) 转换。
  - PLAT 是 464XLAT 中的提供商端转换器。它只不过是一个有状态的 NAT64 网关。
  - 这是 NAT464 转换的唯一明确定义的模型。

- 最后两项与 IPv6/IPv4 共存无关，但为了完整性在此包括：

  - NPTv6（IPv6 到 IPv6 网络前缀转换）是一种*实验性*技术
    \[[RFC6296](https://www.rfc-editor.org/info/rfc6296)\]，其适用性存在争议。

  - NAT66 未由 IETF 定义，并且鉴于 IPv6 地址的大量供应，通常不认为足够有用以克服其缺点，它与经典 IPv4 NAT 共享这些缺点
    \[[RFC5902](https://www.rfc-editor.org/info/rfc5902)\]。像 IPv4 NAT 一样，它可能在支持端口转换（即 NAPT66）的情况下实现，但由于没有 IPv6 地址的短缺，端口转换是不必要的。

### IPv4 即服务的更多详细信息

上面列出的第 2 点显然需要有状态 NAT64
\[[RFC6146](https://www.rfc-editor.org/info/rfc6146)\]。

此外，客户端可以被触发以启动跨协议连接。为此，应该告诉客户端服务器在 IPv6 互联网上可用。DNS64
\[[RFC6147](https://www.rfc-editor.org/info/rfc6147)\] 可以在 ISP 端执行此操作。它可以通过添加特定的静态前缀从 IPv4 地址合成 IPv6 地址。当客户端请求 `www.example.net`（在全局 DNS 中只有 A 记录）时，DNS64 将合成并返回 AAAA 记录。DNS64 的部署涉及复杂性，在 IPv4 即服务的存在下不是必需的。

上面的第 3 点可以通过各种技术实现（除了第 1 点和第 2 点）：

- 464XLAT（有状态和无状态转换的组合）
  \[[RFC6877](https://www.rfc-editor.org/info/rfc6877)\]
- DS-Lite（双栈精简版）
  \[[RFC6333](https://www.rfc-editor.org/info/rfc6333)\]
- lw4o6（轻量级 4over6）
  \[[RFC7596](https://www.rfc-editor.org/info/rfc7596)\]
- MAP E（带封装的地址和端口映射）
  \[[RFC7597](https://www.rfc-editor.org/info/rfc7597)\]
- MAP T（使用转换的地址和端口映射）
  \[[RFC7599](https://www.rfc-editor.org/info/rfc7599)\]。

[RFC 9313](https://www.rfc-editor.org/info/rfc9313) 对这些技术有很好的概述和比较。

下图说明了这样的场景。
<img src="./vasilenko-IPv4aaS.png" alt="User devices connected to Internet via IPv6 infrastructure" width="auto" height="auto"/>

- 464XLAT 现在是广泛首选的转换技术，因为它与 NAT64（本身非常理想）具有天然的协同作用，并且因为它是移动设备上唯一支持的解决方案。集中式 NAT64 引擎称为 PLAT，与普通 NAT64 相同
  \[[RFC6146](https://www.rfc-editor.org/info/rfc6146)\]。客户端称为 CLAT，通常是无状态 NAT46 转换
  \[[RFC7915](https://www.rfc-editor.org/info/rfc7915)\]。对部署考虑因素的良好分析在
  [RFC 8683](https://www.rfc-editor.org/info/rfc8683) 中，运营商可能会从中得出结论*不*实施 DNS64，因为 IPv4 客户端可以简单地使用正常的 DNS A 记录和 IPv4 服务，就好像它是原生的一样。

- DS-Lite 在相当长的一段时间内是最流行的技术。

- Lw6o4 没有获得显著的市场采用。

- 从技术上讲，MAP-E 和 MAP-T 是无状态的，具有显著的相关优势：不需要日志，可以在路由器上实现。但 MAP 需要为所有客户端（即使在断开连接时）保留相当大的 IPv4 地址空间，并且 MAP 在大多数移动操作系统上默认不可用。因此，MAP 的市场份额很小。

### 移动设备的 IPv4 即服务

上图涵盖了网络的 IPv4aaS。一个特殊情况是移动设备的 IPv4aaS，特别是当设备仅被提供单个 /64 前缀时，这在大多数 3GPP 部署中是这种情况。在这种情况下，464XLAT 是唯一可用的解决方案，如
[RFC 6877](https://www.rfc-editor.org/info/rfc6877) 的第 6.3 节所述，CLAT 将使用该 /64 前缀中的特定地址。

### NPTv6 的更多详细信息

网络前缀转换 (NPTv6)
\[[RFC6296](https://www.rfc-editor.org/info/rfc6296)\] 是一种仅在 IPv6 中可用的特殊技术。它在转换引擎的"内部"（专用网络）和"外部"（公共网络）之间交换前缀并修改 IID。IID 被更改以保留传输层校验和，尽管前缀发生了变化。因此，它对所有传输层协议都是透明的。原则上，例如，它将允许使用 ULA 地址的站点
\[[2. 地址](../02.%20IPv6%20Basic%20Technology/Addresses.md)\] 与全局 IPv6 地址通信，但具有经典 IPv4 NAT 的一些缺点，有时称为 1:1 NAT，不要与伪装地址转换混淆。NPTv6 和经典 NAT 之间的主要区别是它允许在两个方向上启动连接。然而，对于在高层嵌入 IP 地址的应用程序（所谓的"引用"），它不是完全透明的。因此，不能认为它是端到端透明的。

一个特殊的困难是，如果没有代理机制的支持，SIP（IP 电话的会话发起协议）将无法在 NPTv6 后面工作
\[[RFC6314](https://www.rfc-editor.org/info/rfc6314)\]。

如上所述，NPTv6 在
[RFC 6296](https://www.rfc-editor.org/info/rfc6296) 中概述；然而，尽管有重要的商业支持，但应该注意的是，在撰写本文时，RFC 是实验性的，因此不被视为标准轨道。

不用说，IPv6 地址短缺_永远_不能证明 NPTv6 是合理的。然而，虽然关于打破 IPv6 中的端到端地址透明度存在争议，但此类架构有有效的用例，打破端到端模型更多是一个不幸的副作用，而不是此类工具的特性。关于 NPTv6 造成的"破坏"的一些细节，以及与经典 NAT 的比较，在
[RFC 6296 的第 5 节](https://www.rfc-editor.org/rfc/rfc6296.html#section-5) 中给出。

在广域架构的大规模部署中，NPTv6 确实实现了一些引人注目的用例，这些用例在安全平台（如有状态统一威胁管理设备 (UTM)）中实现多样性。这些位于地理和拓扑上的不同位置，但需要*外部*第 3 层寻址的灵活性来支持流识别。使用 NPTv6 执行地址重新映射允许检查引擎维护有状态深度数据包检查引擎运行所需的流对称性，因为不对称会导致它们将所有流标记为不完整。正是在这个模型中，它可以是 GUA 到 GUA，这是一个有效的、可支持的、绝对是生产部署的架构。

在较小的部署中，NPTv6 可以用于在网络内部创建稳定的寻址，该网络可能对于 PI 地址空间来说太小，但对于在没有服务提供商多样性的情况下运行来说太大。在这个模型中，例如 SD-WAN 部署，GUA 或 ULA 前缀可以部署，由总部、其他 IT 治理机构或本地管理员委派，并映射到由低成本商业互联网服务提供的一个或多个 PA 前缀。这允许内部寻址保持稳定，同时提供更强大的连接模型，并通过利用映射到内部稳定寻址的外部动态寻址，在需要时更快地切换提供商的能力。该模型更接近于当前几乎无处不在部署的 IPv4 架构，具有稳定的内部 IPv4 寻址，伪装为上游 ISP 提供的一个或多个 PA 地址。

### NAT66 的更多详细信息

NAT66 目前是一种基于非标准的机制，用于有状态地将一个或多个 IPv6 地址转换为一个或多个其他 IPv6 地址。当还提供端口转换时（对于 IPv4 NAT 非常常见），术语 NAPT66 也可以使用。

不用说，IPv6 地址的普遍短缺_永远_不能证明 NAT66 是合理的。像 NPTv6 一样，NAT66 应该只在必要或需要时使用。此外，理解这些工具的意图是转换也非常重要，因此得名。它们可能在合规性要求中发挥作用，但它们在核心上是转换工具，而不是安全机制。地址转换通常与有状态数据包过滤一起部署，但这两者实际上是独占的工具包。也就是说，它们不相互绑定，应该被视为不同的——地址转换不是安全工具。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Tunnels.md) [<ins>下一页</ins>](Obsolete%20techniques.md) [<ins>顶部</ins>](03.%20Coexistence%20with%20Legacy%20IPv4.md)
