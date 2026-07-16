## 路由运维

### 全局路由

使用多协议BGP-4
\[[RFC2545](https://www.rfc-editor.org/info/rfc2545)，
[RFC 4271](https://www.rfc-editor.org/info/rfc4271)，
[RFC 4760](https://www.rfc-editor.org/info/rfc4760)\]
在服务提供商之间进行全局路由是一个高度专业化的主题，不适合业余爱好者，这里不做总结。
一个极好的资源是Iljitsch van Beijnum的书
[BGP互联网路由](https://www.iljitsch.com/2022/11-18-new-e-book-internet-routing-with-bgp.html)
（2022年）。有关相关的RFC和即将发布的草案，请参阅
[IETF GROW工作组](https://datatracker.ietf.org/wg/grow/documents/)，
其涵盖IPv6和IPv4 BGP操作。

### 运营商、企业和园区网络

运营商（互联网服务提供商）和非常大的企业通常操作iBGP
\[[RFC4456](https://www.rfc-editor.org/info/rfc4456)\]，
IS-IS \[[RFC5308](https://www.rfc-editor.org/info/rfc5308)，
[RFC 7775](https://www.rfc-editor.org/info/rfc7775)\]，
或OSPFv3 \[[RFC5340](https://www.rfc-editor.org/info/rfc5340)\]
用于IPv6。

大多数企业网络或园区网络通常操作
OSPFv3 \[[RFC5340](https://www.rfc-editor.org/info/rfc5340)\]
或IS-IS \[[RFC5308](https://www.rfc-editor.org/info/rfc5308)，
[RFC 7775](https://www.rfc-editor.org/info/rfc7775)\]用于IPv6。

有关OSPFv3使用的简要介绍在
[Blueally博客](https://www.blueally.com/ipv6-deployment-series-part-3-ospfv3/)。

不是每个人都能参加RIPE NCC的_高级IPv6_培训课程，但每个人都可以下载他们出色的264张幻灯片，其中涵盖了OSPF和BGP配置以及许多其他内容：
[下载37MB](https://www.ripe.net/documents/3822/AdvancedIPv6-Slides_xDUF4U9.pdf)。

来自Cisco的IS-IS（适用于所有地址族）视频介绍在
[YouTube上](https://youtu.be/jWdD8SCwzHk)。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Benchmarking%20and%20monitoring.md) [<ins>下一页</ins>](Security%20operation.md) [<ins>返回顶部</ins>](06.%20Management%20and%20Operations.md)
