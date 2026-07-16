## 每主机前缀

IPv6 节点通常有多个有效地址，例如通过配置临时地址
\[[RFC8981](https://www.rfc-editor.org/info/rfc8981)\]。由于 IPv6 地址空间不是稀缺资源，因此在某些场景中，向单个主机分配完整的 /64 前缀可能是有利的。此类机制已在
[RFC 8273](https://www.rfc-editor.org/info/rfc8273)、
[RFC 9663](https://www.rfc-editor.org/info/rfc9663)、
[RFC 9762](https://www.rfc-editor.org/info/rfc9762) 和
\[[RFC9818](https://www.rfc-editor.org/info/rfc9818)\] 中定义。

这种解决方案可能有用的一个场景是共享访问网络服务，其中第 2 层访问网络（通常是 Wi-Fi）由多个访问订户设备共享。服务提供商可能有法律或运营要求，需要在连接的访问设备之间提供隔离，例如控制共享网络的潜在滥用。单独的前缀使这种隔离变得更简单，因为不需要跟踪每个主机的多个单独 /128 地址。

这种方法还有其他好处，例如邻居缓存的更好扩展属性等，这些在 RFC 9663 中讨论。后者使用标准的 DHCPv6 前缀委派（DHCPv6-PD）
\[[RFC8415](https://www.rfc-editor.org/info/rfc8415)\]，而 RFC 8273 使用特制的路由器通告消息。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Address%20Planning.md) [<ins>下一页</ins>](../06.%20Management%20and%20Operations/06.%20Management%20and%20Operations.md) [<ins>顶部</ins>](05.%20Network%20Design.md)
