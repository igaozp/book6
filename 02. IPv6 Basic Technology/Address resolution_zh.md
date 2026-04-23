## 地址解析

当IPv6节点"A"得知另一个节点"B"的IPv6地址，并需要向B发送数据包时，它必须首先确定B是否直接连接到与A相同的某个链路上。如果不是，它将需要将数据包发送到路由器（参见[路由](Routing.md)）。这被称为"链上确定"。最简单的情况是当B的地址是[地址](Addresses.md)中描述的链路本地地址。在这种情况下，它必然在链上。在B具有可路由地址的情况下，A可以通过查询从路由器通告（RA）消息接收到的信息来确定它是否在链上。这个过程在
[RFC 4861](https://www.rfc-editor.org/info/rfc4861)中有很好的描述，因此这里不再重复。

当A确定B的地址在链上，并在此过程中确定该链路连接到哪个接口时，它开始地址解析，也称为邻居发现（ND）或邻居发现协议（NDP）。它通过该接口向相关的链路本地多播地址（称为请求节点多播地址）多播一个邻居请求消息。这在
[RFC 4291](https://www.rfc-editor.org/info/rfc4291)中定义，但在
[RFC 4861](https://www.rfc-editor.org/info/rfc4861)中解释。邻居请求是ICMPv6消息的一种特定形式；ICMPv6在
[RFC 8200](https://www.rfc-editor.org/info/rfc8200)中定义。由于这是链路本地多播，此类消息永远不会逃离本地链路。

所有IPv6节点**必须**监听发送到请求节点多播地址的多播。当B收到来自A的邻居请求时，它会回复一个邻居通告ICMPv6消息，单播发送到A的链路本地地址。然后A将解码该消息以获取B的第2层地址（通常是IEEE MAC地址），并将信息记录在其邻居缓存中以供将来使用。此时，A拥有向B发送数据包所需的所有信息。

这些是地址解析的要点；想要了解更多细节的读者应查阅
[RFC 4861](https://www.rfc-editor.org/info/rfc4861)。

这种机制在小规模上运行良好，它的设计充分考虑了在运行IPv4的大型桥接以太网上遇到的"ARP风暴"。然而，它可能会在大型桥接WiFi网络上造成严重的多播过载，并且由于下一节描述的重复地址检测（DAD）的需要而变得更糟。大型WiFi网络对多播的支持很差，正如
[RFC 9119](https://www.rfc-editor.org/info/rfc9119)和
[RFC 5757](https://www.rfc-editor.org/info/rfc5757)第4.2.1节所讨论的。作为最低要求，大型网络中的WiFi基础设施交换机需要支持
[RFC 4541](https://www.rfc-editor.org/info/rfc4541)中解释的*MLD侦听*。"MLD"表示"多播侦听器发现"，是IPv6路由器用来识别哪些节点需要接收发送到给定多播地址的数据包的机制。MLD版本2由
[RFC 3810](https://www.rfc-editor.org/info/rfc3810)规定。当然，所有IPv6节点必须加入`ff02::1`多播组以及相关的请求节点多播组，因此MLD侦听并不能避免扩展问题，但至少它可以抑制不需要多播的WiFi段上的多播。

已经定义了一些优化，例如无偿邻居发现\[[RFC9131](https://www.rfc-editor.org/info/rfc9131)\]，但在这个领域还需要进一步的标准化工作。

过去已经分析了邻居发现和无线多播的运营问题
（[RFC 6583](https://www.rfc-editor.org/info/rfc6583)、
[RFC 6636](https://www.rfc-editor.org/info/rfc6636)、
[RFC 9119](https://www.rfc-editor.org/info/rfc9119)），但事实仍然是，非常大的WiFi网络（例如IETF每年为其全体会议建立的网络）会遭受严重的多播过载。在实践中，这会导致WiFi交换机任意限制多播速率，因此邻居发现进展非常缓慢。**强烈**建议尽可能限制无线子网的大小。

关于无线网络（不仅仅是WiFi）上邻居发现的问题和复杂性的总结可以在
[这份草案](https://datatracker.ietf.org/doc/draft-ietf-6man-ipv6-over-wireless/)中找到。

在低功耗无线个域网（6LoWPAN，使用IEEE 802.15.4标准）的情况下，已经完成了大量工作来缓解这些问题。相关的RFC包括
[RFC 6775](https://www.rfc-editor.org/info/rfc6775)、
[RFC 8505](https://www.rfc-editor.org/info/rfc8505)、
[RFC 8928](https://www.rfc-editor.org/info/rfc8928)、
[RFC 8929](https://www.rfc-editor.org/info/rfc8929)和
[RFC9685](https://www.rfc-editor.org/info/rfc9685)。这些改进可能会在未来更普遍地应用。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Layer%202%20functions.md) [<ins>下一页</ins>](Auto-configuration.md) [<ins>顶部</ins>](02.%20IPv6%20Basic%20Technology.md)
