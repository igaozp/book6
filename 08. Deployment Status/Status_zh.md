## 状态

当谈到IPv6时，一个问题立即出现："目前有多少人在互联网上使用IPv6？"。回答这个问题对于了解IPv6的实际采用情况至关重要。2023年的概述在[RFC 9386](https://www.rfc-editor.org/info/rfc9386)中呈现。

IPv6用户数量由各种组织监控。例如，[Facebook](https://www.facebook.com/ipv6/?tab=ipv6_total_adoption)和[Google](https://www.google.com/intl/en/ipv6/statistics.html)都提供了通过IPv6访问其服务的用户统计数据。由于使用的方法不同，结果也不同。Google通常看到比Facebook更多的IPv6使用，但Google在中国有一个盲点，而那里的采用率很高。

区域互联网注册机构(RIR)的可信来源是[APNIC Labs](https://stats.labs.apnic.net/ipv6/)。该站点测量的是能力而非流量或活跃用户，因此这些数据不应与Google或Facebook直接比较。APNIC通过在互联网浏览器上运行的脚本来量化IPv6的可用性。

[Cloudflare](https://blog.cloudflare.com/ipv6-from-dns-pov)在2023年发布了一篇非常有信息量的博客，显示人类使用IPv6的频率远高于机器人，后者似乎更喜欢IPv4。Cloudflare当前的协议使用数据由[Cloudflare radar](https://radar.cloudflare.com/)汇总。

[Akamai](https://web.archive.org/web/20250324111641/https://www.akamai.com/internet-station/cyber-attacks/state-of-the-internet-report/ipv6-adoption-visualization)以前提供了测量其内容分发平台点击次数的数据。例如，他们显示2024年初印度的采用率为72%。

2025年末，Google、Facebook和Cloudflare大致同意全球用户采用率为40%到50%，APNIC Labs显示IPv6能力为42%。

关于顶级网站的DNS记录和可达性的一些统计数据可以在[Dan Wing的网站](https://www.employees.org/~dwing/aaaa-stats/)找到。这些数据表明，到2025年11月，只有30%的站点拥有IPv6 DNS条目。因此，虽然主要站点看到高达50%的IPv6使用率，但大多数较小的站点甚至还没有参与进来。

在撰写本文时，这些来源和其他来源的数据之间存在显著差异。事实上，对于"存在多少IPv6用户"或"存在多少IPv6流量"并没有明确定义的度量标准。举个例子，Google估计使用IPv6的Google"点击"比例，但Google在中国很少使用，因此这些数据无法代表真正的全球情况。Geoff Huston在2023年7月向IETF发布的估计表明，Google当时在中国观察到7%的采用率，而APNIC测量报告的能力为30%。

我们在这里展示了APNIC的较旧结果展示，以显示几年前的互联网IPv6用户数量，与总互联网人口的比较(以百万计，见下表)。

<img src="./Section5_Table1.jpg" alt="表格显示2018年至2022年IPv6年增长率为25%">

当时互联网人口的三分之一显然采用了IPv6。看看增长曲线也很有趣。这里的主要指标是复合年增长率(CAGR)，显示2018-2022年的5年期间有两位数的增长。

然而，有一个注意事项。由于地方政策过滤来自国外的流量，APNIC使用的方法无法在中国完全使用。一项独立的[中国研究](https://www.china-ipv6.cn/#/activeconnect/simpleInfo)报告称，截至2022年9月，测量的IPv6客户为7.13亿，而APNIC报告的为2.2亿。如果我们将两个统计数据之间的差异添加到全球计数中，我们最终会得到2022年9月43%的使用率。(碰巧的是，当月Google的全球测量峰值为41%。)

2025年8月，中国国家互联网信息办公室宣布，截至6月，中国有8.34亿活跃IPv6用户，即中国互联网用户的75%。移动网络上66%的流量通过IPv6运行，而固定网络上为28%。到2025年10月，[中国媒体声称采用率为77%](https://www.chinadaily.com.cn/a/202510/31/WS690473f6a310f735438b8167.html)。

<!-- Link lines generated automatically; do not delete -->

### [<ins>下一页</ins>](Deployment%20by%20carriers.md) [<ins>顶部</ins>](08.%20Deployment%20Status.md)
