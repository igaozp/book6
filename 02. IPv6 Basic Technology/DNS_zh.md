## DNS

我们假设读者对域名系统（DNS）有良好的总体理解。DNS的许多方面不受IPv6影响，因为它是基于非常通用的原则设计的。

定义了一个特定的资源记录类型来嵌入IPv6地址：AAAA记录\[[RFC3596](https://www.rfc-editor.org/info/rfc3596)\]。这只是以与A记录提供IPv4地址相同的方式提供128位IPv6地址。（AAAA通常发音为"Quad-A"。）

同样，反向查找由`IP6.ARPA`域启用。这是使用表示为十六进制字符的4字节半字节完成的，因此地址`2001:db8:4006:80b:a1b3:6d7a:3f65:dd13`将显示为
`3.1.d.d.5.6.f.3.a.7.d.6.3.b.1.a.b.0.8.0.6.0.0.4.8.b.d.0.1.0.0.2.IP6.ARPA.`
显然，这些条目是为计算机准备的，而不是为人类准备的。

定义AAAA记录的一个必然结果是，*间接*导致A记录查找的DNS查找也必须导致AAAA查找。这涉及NS、SRV和MX查找。

此更改还影响涉及DNS的API调用。旧的`gethostbyname()`和`gethostbyaddr()`调用已**过时**，不应再使用。它们被`getaddrinfo()`和`getnameinfo()`取代，后者处理IPv6和IPv4。特别是，`getaddrinfo()`为程序员提供IPv6和IPv4地址列表，程序员的工作是决定使用哪一个。地址呈现给程序员的顺序由主机上的本地配置表确定，方式在[RFC 6724](https://www.rfc-editor.org/info/rfc6724)中描述。不幸的是，用于此表的远程配置的标准DHCPv6机制\[[RFC7078](https://www.rfc-editor.org/info/rfc7078)\]并未被广泛使用。运营商在尝试让用户偏好IPv6而不是IPv4（或相反）时需要意识到这种复杂性。

除此之外，在理想世界中，IPv6的DNS不应该引起额外的运营问题。然而，在实践中，有一些值得关注的事项：

- 如
  [2. 托管配置](../02.%20IPv6%20Basic%20Technology/Managed%20configuration.md)中所述，
  即使使用DHCPv6，子网的DNS服务器也必须由路由器通告来宣布。

- DNS IPv6传输操作指南记录在
  [BCP 91](https://www.rfc-editor.org/info/bcp91)中。

- 互联网服务提供商的IPv6反向DNS注意事项记录在
  [RFC 8501](https://www.rfc-editor.org/info/rfc8501)中。

- 某些站点使用AAAA记录注册IPv4映射的IPv6地址（例如`::ffff:198.51.100.99`）的情况并非罕见。虽然这在大多数情况下似乎有效，但如果相关主机具有有效的IPv6地址，则这是不适当的，否则就是无意义的。

- 某些IPv6地址类型**永远**不应在全局DNS中可见：ULA（以`fdxx:`甚至`fcxx:`开头）或链路本地（以`fe80::`开头）。请注意，像Active Directory这样的自动化机制可能默认将ULA添加到全局DNS。当然，如果使用拆分DNS配置，将ULA包含在_本地_DNS中是可以的。

  _注意：_DNS中确实存在一些ULA地址的AAAA记录，它们不构成安全风险，但从用户的角度来看，它们可能会导致意外失败。

关于AAAA记录和可达性的一些统计数据可以在
[Dan Wing的网站](https://www.employees.org/~dwing/aaaa-stats/)上找到。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Managed%20configuration.md) [<ins>下一页</ins>](Routing.md) [<ins>顶部</ins>](02.%20IPv6%20Basic%20Technology.md)
