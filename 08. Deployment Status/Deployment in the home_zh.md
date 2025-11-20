## 家庭部署

很难估计在给定日期有多少比例的家庭用户拥有IPv6连接。[Google](https://www.google.com/intl/en/ipv6/statistics.html)的统计数据很有趣，因为它们清楚地显示了IPv6访问的周末峰值(2023年4月高达43%)，表明家庭和/或移动IPv6连接水平相当高。

市场上用于家庭(或小型办公室)使用的设备中，有些但不是全部同时支持IPv6和IPv4。然而，较旧的设备只有IPv4。因此，今天典型的家庭网络运行双栈。此外，典型的网络不包括多个子网；存在的唯一路由器同时是子网路由器和CE路由器。假设ISP支持IPv6，无论它是提供原生IPv4还是IPv4即服务，路由器都在LAN上提供双栈服务。LAN本身通常是WiFi，可能桥接到以太网。(即使CE路由器根本不支持IPv6，链路本地IPv6也应该可以工作。)

因此，事情相当简单。PC和打印机等设备可以使用任何可用的方式相互通信 -- IPv4、链路本地IPv6或全局IPv6。(例如：2019年安装的Windows 10 PC使用链路本地IPv6与2022年安装的Canon喷墨打印机通信，无需手动配置。)对于在DNS中具有AAAA地址的服务，将优先使用IPv6建立与互联网的连接，否则使用IPv4。这些连接可能会通过Happy Eyeballs技术\[[RFC8305](https://www.rfc-editor.org/info/rfc8305)\]进行优化。大多数家庭用户对所有这些将基本上保持无知。

当考虑各种家庭自动化设备时，情况变得更加复杂，特别是如果希望将家庭网络拆分为单独的子网时。这样的网络需要基本上是自配置和自管理的，物联网网络也是如此。这些复杂的主题超出了本书的范围。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Deployment%20by%20carriers.md) [<ins>下一页</ins>](Deployment%20in%20the%20enterprise.md) [<ins>顶部</ins>](08.%20Deployment%20Status.md)
