## 地址和前缀管理

可以区分三种主要情况：

1. 非托管网络通常会在服务提供商分配给它们的子网前缀内使用无状态地址自动配置（SLAAC，
   [RFC 4862](https://www.rfc-editor.org/info/rfc4862)）。这与IPv4实践形成对比，在IPv4中，DHCP在大多数非托管网络中自动配置。

1. 提供商网络通常会根据
   \[[5. 地址规划](../05.%20Network%20Design/Address%20Planning.md)\]中讨论的预定义计划，在网络元素（包括客户网关）上配置前缀和地址。
   DHCPv6前缀委派 `OPTION_IA_PD` 可用于向路由器分配前缀，即使DHCPv6不用于地址分配
   \[[2. 托管配置](../02.%20IPv6%20Basic%20Technology/Managed%20configuration.md)\]。

1. 托管企业网络将准备满足其特定要求的地址和子网计划。举一个非常简单的例子，ISP给予企业一个/48前缀，企业可能会为每个分支机构分配一个/56，然后根据需要在每个分支内分配/64子网。然后必须决定是在整个网络中部署SLAAC，还是使用DHCPv6 `OPTION_IA_NA` 进行地址分配
   \[[2. 托管配置](../02.%20IPv6%20Basic%20Technology/Managed%20configuration.md)\]。
   这一选择对故障排除和安全事件管理都有影响。

当帮助台电话或安全警报涉及特定的IPv6地址时，响应者需要知道涉及哪台计算机和哪个用户。在某些安全案例中，这可能具有财务影响，并可能需要满足取证证据标准。因此，确定地址、设备和用户之间的对应关系是许多企业的硬性要求。这也被称为_地址问责制_。

在SLAAC的情况下，IPv6地址与已连接设备的MAC地址之间的对应关系嵌入在同一链路上其他设备（包括子网路由器）的邻居发现缓存中。这是易失性信息，特别是如果正在使用IPv6临时地址
\[[RFC8981](https://www.rfc-editor.org/info/rfc8981)\]或可变MAC地址\[[RFC9724](https://www.rfc-editor.org/info/rfc9724)\]。这个主题在
[RFC 9099](https://www.rfc-editor.org/info/rfc9099)的第2.6.1.4节中讨论。需要一个补充机制以适当的频率提取和记录这些信息。另一种选择是持续监控邻居发现流量并提取和记录相同的信息。还观察到监控DAD（重复地址检测）流量也可以工作，如
[此博客](https://weberblog.net/monitoring-mac-ipv6-address-bindings/)中所述。
所有这些解决方案对于大型企业都有令人不快的扩展属性。一种新方法是主机使用DHCPv6主动注册自生成的IPv6地址
\[[RFC9686](https://www.rfc-editor.org/info/rfc9686)\]。

在由DHCPv6分配地址的情况下，IPv6-MAC地址对应关系嵌入在DHCP服务器配置中。在最简单的方法中，MAC地址被预先注册，既不支持临时IPv6地址也不支持可变MAC地址。然而，这使网络暴露于攻击之下，因为使用大多数现代设备伪造MAC地址是微不足道的。

无论使用SLAAC还是DHCPv6，未知MAC地址的用户都可以通过IEEE 802.1X访问控制进行身份验证，这将在正在使用的MAC地址与用于身份验证的人类用户凭据之间提供强有力的联系。

另一个因素是，一个广泛使用的主机操作系统Android目前不支持通过DHCPv6进行主机地址分配。对于双栈部署，一种解决方案是接受受影响的设备将仅使用IPv4。另一种是为"自带设备"（BYOD）提供单独的WiFi BSS，其中SLAAC可用，但此网络将被视为可疑网络，并将有效地位于企业防火墙之外。第三种解决方案是根本不为此类设备提供服务，这些设备将不得不连接到公共蜂窝系统。

网络运营商必须在SLAAC和DHCPv6之间做出有意识的选择，并结合其对IPAM（IP地址管理）解决方案的选择（如适用）。一个重要的问题是，是否存在工具来满足上述帮助台和安全需求_针对正在使用的特定供应商设备和软件_。

本书不推荐特定产品。但是，应该注意的是，确实存在支持基于DHCPv6的地址管理（包括动态DNS）的[开源解决方案](https://www.isc.org/kea/)。

<!-- Link lines generated automatically; do not delete -->

### [<ins>下一页</ins>](Remote%20configuration.md) [<ins>返回顶部</ins>](06.%20Management%20and%20Operations.md)
