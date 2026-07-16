## 工具

<!-- ## Chapter X: IPv6 Diagnostic Tools -->

有效的 IPv6 管理和故障排除在很大程度上依赖于专业的诊断工具。虽然基本的网络诊断工具（如 `ping` 和 `traceroute`）在 IPv4 和 IPv6 中的功能类似，但存在一些关键的细微差别以及专门为 IPv6 定制的附加工具。

### 基本 IPv6 工具

常见的网络实用程序（如 `ping` 和 `traceroute`）通常同时支持 IPv4 和 IPv6。但是，由于历史原因，某些操作系统维护单独的 IPv6 特定实用程序，如 `ping6` 和 `traceroute6`。了解哪个版本适用于您的系统至关重要。

```bash
# 基本 IPv6 ping
ping6 3fff:0:1::1

# IPv6 traceroute
traceroute6 3fff:0:1::1
```

### IPv6/IPv4 转换注意事项

当使用 NAT64 和 DNS64 等转换机制时，传统工具（如 traceroute 或在线 IP 检查器）可能会报告 IPv4 地址，即使在测试 IPv6 连接时也是如此。通过确认转换配置来确保对这些结果的正确解释。

### 专业 IPv6 工具

#### radvdump

`radvdump` 是一个旨在捕获和显示 IPv6 路由器通告消息的实用程序，对于分析路由器配置和检测通告问题至关重要。

```bash
sudo radvdump
```

#### scapy

`scapy` 是一个功能强大的基于 Python 的交互式数据包操作程序，支持 IPv6。它对于自定义数据包制作、网络测试和故障排除非常有价值。如果更倾向于工具创建，可以使用它，但它为包含在自定义或特定学科任务中提供了一组强大的功能。

```python
from scapy.all import *
send(IPv6(dst="3fff:0:1::1")/ICMPv6EchoRequest())
```

#### pcap 工具

数据包捕获工具（如 `tcpdump` 和 Wireshark）对于诊断 IPv6 连接问题、检查网络流量和验证协议行为至关重要。

```bash
# 捕获 IPv6 流量
sudo tcpdump -i eth0 ip6
```

Wireshark 提供图形界面，提供专门针对 IPv6 优化的详细数据包解码和分析。

#### 基于 Web 的工具

基于 Web 的 IPv6 工具提供快速诊断，检查 IPv6 连接、DNS 配置以及从全球互联网的可达性。

- 测试 IPv6 连接：[https://test-ipv6.com](https://test-ipv6.com)
- IPv6 DNS 查找和测试：
  [https://ipv6-test.com](https://ipv6-test.com)

#### mtr

`mtr` 将 ping 和 traceroute 的功能组合到一个工具中，提供有关网络路径质量和延迟的实时统计信息，并且支持 IPv6。

```bash
mtr -6 3fff:0:1::1
```

#### IPv6 寻址和第 2 层/第 3 层映射工具

IPv6Utils 是一个命令行实用程序，提供多种工具，包括对地址规划有用的子网生成，以及使用 RFC 6052 的 IPv4/IPv6 地址转换、EUI-64 解码、链路本地解码。它还作为具有相同功能的在线服务提供。

- [https://github.com/buraglio/ipv6utils](https://github.com/buraglio/ipv6utils)

- [https://tools.forwardingplane.net](https://tools.forwardingplane.net)

`ndisc6` 是一个 Linux 软件包，包含用于理解和排除 NDP（邻居发现协议）故障的有用工具。特别是，二进制文件 `ndisc6` 和 `rdisc6` 分别用于生成通过特定接口针对特定地址的邻居请求和路由器请求数据包。这对于强制 Linux 系统从用户空间任意尝试对 IPv6 主机进行地址解析非常有用，即使内核的 NDP 条目不需要刷新也是如此。二进制文件 `ndisc6` 大致相当于 IPv4 工具 `arping` 的 IPv6 版本。`rdisc6` 二进制文件具有类似的功能，但发送和接收 RS/RA 消息而不是 NS/NA 消息。如果您发现自己需要生成 NDP 消息而不想从头开始构建整个数据包（例如，使用 `scapy`），或者想要快速查看由第 2 层相邻 IPv6 主机生成的 NA/RA 消息的内容，或者只是想让第 2 层相邻主机发送您计划使用其他工具（如 `tcpdump` 或 `wireshark`）查看的 NA/RA，这些工具会很有用。

- [https://github.com/nomis/ndisc6](https://github.com/nomis/ndisc6)

#### ASN 查找工具

ASN（自治系统号）工具帮助网络管理员将 IPv6 地址追溯到其原始 AS，协助故障排除、识别路由问题和验证 BGP 配置。

- 命令行 ASN 查找：

```bash
whois -h whois.cymru.com "-v 3fff:0:1::1"
```

- 基于 Web 的 ASN 查找：
  - [https://bgp.he.net](https://bgp.he.net)
  - [https://asn.cymru.com](https://asn.cymru.com)

利用这些 IPv6 特定的诊断工具可确保在启用 IPv6 的环境中实现强大的网络性能和高效的问题解决。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Advanced%20Troubleshooting.md) [<ins>下一页</ins>](../10.%20Obsolete%20Features%20in%20IPv6/10.%20Obsolete%20Features%20in%20IPv6.md) [<ins>顶部</ins>](09.%20Troubleshooting.md)
