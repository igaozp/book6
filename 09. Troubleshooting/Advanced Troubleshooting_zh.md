## 高级故障排除

- **组播侦听器发现（MLD）：** 确保组播侦听器正常运行，因为 NDP 严重依赖组播。

- **防火墙和 ACL 验证：** 确保防火墙或访问控制列表（ACL）允许必要的 IPv6 流量。

防火墙策略应尽可能在协议之间匹配。ICMPv6 是一个值得注意的例外，因为其显著差异以及对 ICMPv6 的显著依赖使其成为正常 IPv6 功能所必需的。

### 双栈网络故障排除

在双栈环境中，解决同时运行 IPv4 和 IPv6 所产生的复杂性至关重要：

- **协议偏好问题：** 识别应用程序或主机可能错误地偏好 IPv4 而非 IPv6，或反之的情况。

  ```bash
  # 检查路由偏好
  getent ahosts example.com
  ```

- **服务可用性：** 验证网络服务（DNS、DHCP、Web 服务）对 IPv4 和 IPv6 请求的正确响应。

  ```bash
  dig A example.com
  dig AAAA example.com
  ```

- **性能基准：** 持续监控双栈性能以检测和修复次优的 IPv6 连接。

### 快乐眼球算法

"快乐眼球"算法（RFC 8305）通过动态选择提供最佳用户体验的协议来优化双栈体验：

- **行为分析：** 观察应用程序发起的连接，并验证当 IPv6 连接较差或失败时，它是否适当地回退到 IPv4。
- **超时调整：** 调整应用程序内的计时器，以优化 IPv4 回退速度和 IPv6 偏好之间的平衡。
- **诊断工具：** 利用浏览器开发者工具或数据包捕获（Wireshark、tcpdump）实时监控应用程序行为。

### 转换机制故障排除

**DNS64**\
通过确保为仅 IPv4 服务合成 AAAA 记录来验证 DNS64 功能。使用以下命令监控响应：

```bash
dig AAAA ipv4-only-domain.example
```

**NAT64**\
使用状态表和数据包捕获确认 NAT64 转换，以验证正确的地址和端口映射。

```bash
# 检查 NAT64 映射
show nat64 translations
```

**pref64**\
检查主机用于确定 NAT64 前缀的前缀发现机制。

```bash
ip -6 route show
```

### 纯 IPv6 网络

在纯 IPv6 环境中验证服务和应用程序兼容性。测试 DNS、DHCPv6，并确保不存在 IPv4 依赖：

```bash
ping6 ipv6-only-host.example
```

### 组播问题

**无线和无线控制器**\
确保在无线控制器上正确允许和配置组播流量，以支持 IPv6 组播应用程序。

**路由器通告问题**\
检查路由器通告（RA）的正确传播，确保路由器通告正确的前缀和默认路由：

```bash
tcpdump -i eth0 icmp6 and ip6[40] == 134
```

### 基于主机的防火墙

检查主机防火墙规则以验证它们允许必要的 IPv6 流量（ICMPv6、DHCPv6 和所需的应用程序端口）：

```bash
iptables -L -n -v -6
```

### ICMPv6 和过滤

ICMPv6 对 IPv6 功能至关重要，包括路径 MTU 发现、邻居发现和诊断。确保 ICMPv6 消息被允许并正确处理：

```bash
tcpdump icmp6
```

<!-- Link lines generated automatically; do not delete -->

### [<ins>下一页</ins>](Tools.md) [<ins>顶部</ins>](09.%20Troubleshooting.md)
