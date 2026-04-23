## 托管配置

主机地址和其他IPv6参数可以使用IPv6动态主机配置协议（DHCPv6）进行配置。DHCPv6中的参与者是客户端（要配置的主机）、服务器（提供配置数据）以及可选的DHCPv6中继代理，将主机间接连接到主服务器。

人们有时想知道为什么SLAAC和DHCPv6都存在。原因部分是历史性的（IPv4的DHCP在设计IPv6时是新的且未广泛部署）。此外，SLAAC（上一节）的概念旨在避免在简单网络中需要单独的配置协议。结果是即使在复杂网络中，邻居发现和路由器通告消息仍然是必需的，即使部署了DHCPv6。

Android操作系统不支持DHCPv6。这意味着需要支持Android主机的网络必须提供SLAAC以及DHCPv6。在企业环境中，这可能导致运营商运行一个支持SLAAC的单独（WiFi）网络，与使用DHCPv6管理的其他企业网络隔离。或者，他们可能根本不为Android用户提供IPv6支持。蜂窝移动服务提供商确实支持通过从网络到移动设备的点对点3GPP链路上的SLAAC。咖啡店和酒店等公共网络，如果它们支持IPv6的话，也是通过SLAAC来实现的。因此，DHCPv6的适用领域主要是企业网络。他们倾向于偏好托管地址，因为安全合规要求。

DHCPv6由
[RFC 8415](https://www.rfc-editor.org/info/rfc8415)定义。它在概念上类似于IPv4的DHCP，但细节不同。使用时，每个主机必须包含一个DHCPv6客户端，并且子网上必须有一个DHCPv6服务器或DHCPv6中继可用。DHCPv6可以提供分配的IPv6地址和其他参数，并且可以定义新选项。（所有注册的DHCP参数可以在
[IANA网站](https://www.iana.org/assignments/dhcpv6-parameters/dhcpv6-parameters.xhtml#dhcpv6-parameters-2)上找到。）DHCPv6消息使用端口546和547通过UDP/IPv6传输。

DHCPv6的一个显著特点是它可以在*路由器之间*使用以动态分配前缀。例如，如果一个新段被打开并且其路由器没有IPv6前缀，拓扑中"上方"的基础设施路由器可以使用`OPTION_IA_PD`和`OPTION_IAPREFIX` DHCPv6选项为其分配一个（例如/64前缀）（以前由RFC3633定义，但现在由
[RFC8415的第6.3节](https://www.rfc-editor.org/rfc/rfc8415.html#section-6.3)涵盖）。
此过程称为DHCPv6-PD（用于"前缀委派"）。此外，可以在SLAAC路由器通告中发出DHCPv6-PD的可用性信号\[[RFC9762](https://www.rfc-editor.org/info/rfc9762)\]，这允许大型广播网络中的客户端设备受益于每个设备一个IPv6前缀
\[[RFC9663](https://www.rfc-editor.org/info/rfc9663)\]，
\[[5. 每主机前缀](../05.%20Network%20Design/Prefix%20per%20Host.md)\]。

然而，用于蜂窝移动系统上IPv6使用的3GPP规范使DHCPv6和DHCPv6-PD都是可选的
\[[RFC7066](https://www.rfc-editor.org/info/rfc7066)\]，经验表明许多常见的3GPP实现不支持它们。因此，移动设备只能依赖基于RA的地址和前缀机制。

DHCPv6消息类型包括：

- SOLICIT（发现DHCPv6服务器）
- ADVERTISE（对SOLICIT的响应）
- REQUEST（客户端请求配置数据）
- REPLY（服务器发送配置数据）
- RELEASE（客户端释放资源）
- RECONFIGURE（服务器更改配置数据）

DHCPv6选项包括：

- 客户端标识符选项
- 服务器标识符选项
- 非临时地址身份关联选项
- 临时地址身份关联选项
- IA地址选项
- 认证选项
- 服务器单播选项
- 状态码选项
- DNS递归名称服务器选项
- 域搜索列表选项
- 前缀委派身份关联选项
- IA前缀选项

想要了解更多细节的读者应直接查阅
[RFC 8415](https://www.rfc-editor.org/info/rfc8415)。请注意，这是一个约150页的非常复杂的RFC。此外，定义的消息和选项的完整列表可以在
[IANA](https://www.iana.org/assignments/dhcpv6-parameters/dhcpv6-parameters.xhtml)找到，并引用了相关的RFC。

DHCPv6缺少的一个选项是关于默认路由器的信息；这仅通过RA可用，如前几节所述。IETF尚未就通过DHCPv6提供此信息达成共识。事实上，DHCPv6旨在补充路由器通告信息，并不打算在没有路由器的子网上工作。因此，DHCPv6分配的地址实际上具有前缀长度/128，客户端需要将该信息与RA信息结合起来以与其他链上主机通信。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Auto-configuration.md) [<ins>下一页</ins>](DNS.md) [<ins>顶部</ins>](02.%20IPv6%20Basic%20Technology.md)
