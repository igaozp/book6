## 运营商部署

所有提供或使用互联网连接服务的组织都有一个关联的自治系统编号(ASN)。[APNIC](https://blog.apnic.net/2022/01/06/bgp-in-2021-the-bgp-table/)提供了关于全球ASN中IPv6支持演进的统计数据，这些数据是通过观察互联网路由表得出的。

<img src="./Section5_Table2.jpg" alt="表格显示2018年至2022年IPv6年增长率为18%">

支持IPv6的ASN百分比逐年增长，这是一个好迹象。另一方面，该表格没有区分不同行业的采用程度，即ASN是与运营商、服务提供商还是企业相关联。要深入了解这一层面，需要查看更详细的统计数据，例如[Akamai](https://www.akamai.com/internet-station/cyber-attacks/state-of-the-internet-report/ipv6-adoption-visualization)或[APNIC](https://stats.labs.apnic.net)提供的数据。

毫不奇怪，全球绝大多数运营商已经支持IPv6。然而，存在差异。一般来说，在IPv6采用率较高的国家中活跃的运营商也显示出更高的IPv6使用率。例如，根据Akamai的统计数据，美国的IPv6采用率为51%。AT&T、Comcast、T-Mobile和Verizon等运营商的IPv6使用率均超过70%。在欧洲，比利时和德国的IPv6流量均达到50%。Proximus、Telenet、DT、Telefonica Germany、Versatel和Vodafone Germany的比例从50%到70%不等。印度显示出51%的IPv6采用率。那里的运营商也有很高的IPv6使用率。Bharti、Reliance Jio和Vodafone India的比例在60%到70%之间。

虽然不能一概而论，但在IPv6采用率较低的国家，本地运营商启用IPv6的速度往往也较慢。例如，西班牙、意大利和波兰等欧洲国家的采用率分别为4.5%、7%和13.5%。根据APNIC数据，除了Telefonica de España(26%)、Vodafone Italy(21%)、Wind/3 Italy(22%)和Orange Poland(23%)这些例外情况外，所有其他运营商的采用率都远低于20%的门槛。

有线和无线运营商之间也存在差异。后者在IPv6方面通常更先进。在某些情况下\[[RFC9386](https://www.rfc-editor.org/info/rfc9386)\]，它们转向IPv6的原因是缺乏公共IPv4地址。这些运营商决定制定战略计划以启用纯IPv6底层服务，例如通过采用464XLAT等转换机制(Reliance Jio、T-Mobile)，保证传统的IPv4即服务支持。有线领域早期采用IPv6的显著例子是美国的Comcast和英国的Sky。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Status.md) [<ins>下一页</ins>](Deployment%20in%20the%20home.md) [<ins>顶部</ins>](08.%20Deployment%20Status.md)
