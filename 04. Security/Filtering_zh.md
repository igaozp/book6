## 过滤

过滤是安全互联网连接的重要组成部分。由于分层地址规划，IPv6 过滤通常可能很容易。然而，每个过滤器几乎总是消耗产品中四倍的资源。如果设备配置不足，这可能会影响可扩展性或性能。

大多数实践在采用 IPv6 时不会改变：

- [BCP 38](https://www.rfc-editor.org/info/bcp38) 建议运营商基于入口流量的*源*地址进行过滤，以防止地址欺骗。允许来自委派给该客户的范围内的源地址；其他源地址应该被过滤（除了 \[[6. 多前缀操作](../06.%20Management%20and%20Operations/Multi-prefix%20operation.md)\] 中提到的情况）。不实施 BCP38 的运营商是在纵容地址欺骗。
- 根据 [RFC 6890](https://www.rfc-editor.org/info/rfc6890)，应在周边过滤"火星"地址。在 IPv6 的情况下，这是指 [IANA IPv6 特殊用途地址注册表](https://www.iana.org/assignments/iana-ipv6-special-registry/iana-ipv6-special-registry.xhtml)。
- [BGP 对等](https://www.rfc-editor.org/info/rfc7454) 和 [RPKI](https://www.rfc-editor.org/info/rfc8210) 的过滤对 IPv6 不变。
- 路由器的控制平面保护 \[[RFC6192](https://www.rfc-editor.org/info/rfc6192)\] 对 IPv6 或 IPv4 都是通用的。
- [远程触发黑洞](https://www.rfc-editor.org/info/rfc5635) 对 IPv4 和 IPv6 是相同的，除了 IPv6 的前缀 [100::/64](https://www.rfc-editor.org/info/rfc6666) 已经单独定义。
- 所有 IGP 协议应该根据 [RFC 5082](https://www.rfc-editor.org/info/rfc5082) 过滤本地链路的公告。在 IPv6 的情况下，这意味着只允许来自链路本地地址的公告。
- 推荐使用 [DNSSEC](https://www.rfc-editor.org/info/rfc4641)，与 A 或 AAAA 请求无关。

一些过滤器是 IPv6 特有的。

最大的区别与典型的前缀大小（/64）有关。过滤任何长于此的前缀都是无用的，因为主机可能生成不可预测的临时地址。此外，如果希望过滤一个订户，可能适合过滤甚至更短的前缀，例如 /56。建议最初过滤 /64，然后监控情况；如果问题持续存在，则过滤 /60，然后是 /56。/48 是可能属于普通订户的最大前缀，因此过滤更短的前缀来阻止单个订户是没有意义的。

组织的地址规划设计可能不同，包括使用 DHCPv6 配置的 /128 地址，但从外部永远无法知道这一点。如果组织使用 SLAAC，那么 /64 再次是有意义过滤的最小值。

不同范围的地址应该在相应的边界处过滤：

- 根据 [IPv6 地址架构](https://www.rfc-editor.org/info/rfc4291)，LLA 不应该转发到链路之外，
- 根据 [RFC 4193](https://www.rfc-editor.org/info/rfc4193)，ULA 应该在组织边界处过滤，
- 根据 [IPv6 地址架构](https://www.rfc-editor.org/info/rfc4291)，组播地址定义了 5 个范围（接口、链路、管理、站点和组织），应该在相应的边界处过滤。对于最低的范围，边界是明显的，并且通常硬编码到节点中。对于具有灵活边界的范围（如管理、站点、组织），需要特殊配置。

PMTUD 操作在 IPv6 中更重要，因为在传输过程中禁止分片。因此，ICMP 过滤在 IPv6 中可能造成更大的危害。[ICMPv6 过滤建议](https://www.rfc-editor.org/info/rfc4890) 中讨论了应该丢弃或允许什么。

安全设备和目标节点应该检查第一个分片是否包含所有头部（包括传输层），并且根据 [RFC 8200](https://www.rfc-editor.org/info/rfc8200)，分片不应该有重叠。

[带扩展头的数据包的过滤建议](https://www.rfc-editor.org/info/rfc9288) 面向传输情况，其中过度过滤很常见。该 RFC 说明了应该允许、丢弃、拒绝（带 ICMP）、速率限制或忽略哪些特定的 EH。重要的是要提到，这些额外的操作是在 [RFC 7045](https://www.rfc-editor.org/info/rfc7045) 的基本规则之外推荐的，即默认允许在传输中传输所有扩展头。

限制链路上的 ND 消息在 [<ins>地址解析<ins>](../02.%20IPv6%20Basic%20Technology/Address%20resolution.md) 中讨论。

主机中编程的 IPv6 优先级对仅 IPv4 网络造成风险。恶意节点激活 IPv6 可能会造成安全问题。[IPv4 网络上 IPv6 的安全影响](https://www.rfc-editor.org/info/rfc7123) 讨论了在这种情况下需要阻止什么。这些主要是可能有助于绕过周边安全的不同隧道协议，以及用于中间人攻击的流氓 DHCP 或路由器代码。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Layer%202%20considerations.md) [<ins>下一页</ins>](Topology%20obfuscation.md) [<ins>顶部</ins>](04.%20Security.md)
