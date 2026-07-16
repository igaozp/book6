## 第二层注意事项

IPv6 在链路层相对灵活。灵活性通常伴随着复杂性，这可能会带来安全挑战。

最初，人们认为加密的安全邻居发现（SEND，[RFC 3971](https://www.rfc-editor.org/info/rfc3971)）将解决大多数邻居发现风险。不幸的是，SEND 没有被市场接受。因此，[RFC 3756](https://www.rfc-editor.org/info/rfc3756) 第 4.1 节中讨论的安全问题仍然存在：

- 恶意节点可以响应合法节点的任何重复地址发现（DAD）请求，相当于拒绝服务攻击；
- 恶意节点可以污染另一个节点（尤其是路由器）的邻居缓存，以拦截指向另一个节点的流量（中间人攻击）；在许多不同情况下，邻居请求和邻居通告都可能发生这种情况。

这与 IPv4 ARP 欺骗没有太大区别。当然，只有在坏人成功植入恶意节点时，危险才会存在。如果认为这是一个重大风险，最强的保护方法是在单独的链路上使用单独的专用 /64 前缀隔离主机。IPv6 有足够的地址空间来遵循这种策略。所有订户（包括移动订户）已经至少有一个 /64 前缀。/56 前缀被认为是普通家庭订户的最小值，对于小型企业甚至可以使用 /48。后者理论上允许 65,535 个主机各自拥有自己的 /64。

另一种保护方法是源地址验证改进（SAVI）——参见 [RFC 6620](https://www.rfc-editor.org/info/rfc6620)，它基于交换机对完整邻居发现（ND）交换的监控来动态安装过滤器。与 SEND 一样，这不是一个非常流行的解决方案。

蜂窝移动链路（3GPP 等）始终是点对点隧道。因此，可以大大简化 ND 协议（地址解析和 DAD 是不必要的），以避免复杂性和大多数安全威胁——参见 [RFC 7849](https://www.rfc-editor.org/info/rfc7849)。

与 IPv4 一样重要的是限制谁可以声明默认路由器和 DHCP 服务器功能，因为这是组织中间人攻击的最佳方式。因此，定义了 RA-Guard [RFC 6105](https://www.rfc-editor.org/info/rfc6105) 和 DHCPv6-Shield [RFC 7610](https://www.rfc-editor.org/info/rfc7610)。不幸的是，可以通过在传输层前面添加扩展头（特别是危险的分片）来隐藏数据包的目的。因此，[RFC 7113](https://www.rfc-editor.org/info/rfc7113) 和 [RFC 7112](https://www.rfc-editor.org/info/rfc7112) 是防止流氓路由器或 DHCP 所额外需要的。

存在一个与 IPv6 特别相关的新安全攻击向量。SLAAC 地址获取是分布式的，因此即使路由器监控所有 ND 交换，路由器也可能不知道链路上配置的所有地址。因此，路由器需要在从外部源接收到新会话的第一个数据包后请求地址解析。同时，默认情况下，IPv6 链路地址空间是巨大的（2^64）。因此，有可能强制路由器执行大量次数的地址解析（甚至来自外部网络）。这是一种有效的 DoS 攻击，但有简单的保护措施。[RFC 6583](https://www.rfc-editor.org/info/rfc6583) 讨论了如何限制地址解析请求的数量或最小化子网大小。

ND 严重依赖组播，这可能在无线环境中造成问题。参见 [2. 地址解析](../02.%20IPv6%20Basic%20Technology/Address%20resolution.md) 和 [组播效率](https://datatracker.ietf.org/doc/draft-vyncke-6man-mcast-not-efficient)。ND DoS 活动可能因此而有效，但攻击者应该是链路本地的。因此，周边安全可能会有所帮助。在有线环境中，由于链路上通常实现了 MLD 窥探（[RFC 4541](https://www.rfc-editor.org/info/rfc4541)），组播风暴不太成问题。

IPv6 有一个改善隐私的新功能。IPv6 主机通常在同一接口上有许多 IP 地址，通常具有不可预测的（伪随机）IID 值。某些 IP 地址可能暂时使用（[RFC 8981](https://www.rfc-editor.org/info/rfc8981)），这对中间互联网节点跟踪可疑用户活动构成挑战，原因与它保护隐私的原因相同。

<!-- Link lines generated automatically; do not delete -->

### [<ins>下一页</ins>](Filtering.md) [<ins>顶部</ins>](04.%20Security.md)
