## 数据包大小与巨型帧

### 分片

如
[3. IPv6与IPv4的主要区别](../03.%20Coexistence%20with%20Legacy%20IPv4/IPv6%20primary%20differences%20from%20IPv4.md)中已经指出的，IPv6不允许中间路由器对数据包进行分片。相反，IPv6将分片的责任推给源节点。如果数据包超过MTU，它要么由发送方分片，要么被丢弃。这意味着发送方必须使用PMTUD
\[[RFC7690](https://www.rfc-editor.org/info/rfc7690)\]来确保数据包的大小适合路径上最小的MTU。如有必要，发送方在发送数据包之前对其进行分片。这需要发送方进行额外的计算来分片数据包，但没有报告重大性能影响。

### MTU大小和巨型帧

巨型帧是大于标准1500字节的以太网帧，通常配置为约9000字节。如果在IPv4网络中发送巨型帧时，路径上的路由器具有较小的MTU，它将分片该帧。这可能导致更高的分片开销，因为原始帧越大，必须分成的片段就越多。此外，分片在路由器和发生重组的目标处都增加了处理复杂性。

IPv6通过依赖PMTUD
\[[RFC7690](https://www.rfc-editor.org/info/rfc7690)\]避免了这种分片开销。如果巨型帧超过任何网络跳的MTU，发送方负责在传输前对其进行分片。但是，如果配置正确，只要整个路径支持巨型帧，发送方就可以有效地发送较大的数据包而无需分片。这使得IPv6能够更有效地处理较大的数据包，因为路径MTU发现机制确保数据包适合路由上每个跳的MTU。此机制在
\[[RFC8201](https://www.rfc-editor.org/info/rfc8201)\]中定义。

IPv6中的"巨型负载选项"
\[[RFC2675](https://www.rfc-editor.org/info/rfc2675)\]允许传输大于65,535字节（标准IPv6数据包的最大负载大小）的数据包。此选项包含在逐跳选项头中，使IPv6能够有效地支持超级巨型帧，即使在处理极大的数据包大小时也是如此。此机制简化了大数据包的处理，而无需将它们拆分为较小的片段。如果网络支持足够大的MTU，IPv6可以使用此选项来传输大帧而无需中间分片。但是，它很少使用，因为它需要支持非常大数据包的第2层技术。一个有趣的用例是用于支持分段卸载的_内部_通信，如
[此博客条目](https://www.sipanda.io/post/segmentation-offload-and-protocols-let-s-be-friends)中所述。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Energy%20consumption.md) [<ins>下一页</ins>](Basic%20Windows%20commands.md) [<ins>返回顶部</ins>](06.%20Management%20and%20Operations.md)
