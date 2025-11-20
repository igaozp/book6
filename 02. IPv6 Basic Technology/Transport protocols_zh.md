## 传输协议

应用程序可以很容易地更新以在双栈模式下工作，因为传输层受IPv6的影响很小。因此，IPv6支持所有常见的传输协议：

- UDP。UDP over IPv6没有单独的规范；
  [RFC 768](https://www.rfc-editor.org/info/rfc768)仍然适用！
  但是，UDP校验和对于IPv6是强制性的（因为IPv6头本身没有校验和），除非
  [RFC 6936](https://www.rfc-editor.org/info/rfc6936)允许。

- UDP-lite \[[RFC3828](https://www.rfc-editor.org/info/rfc3828)\]也支持IPv6。
  [RFC 8304](https://www.rfc-editor.org/info/rfc8304)中有关于UDP和UDP-lite的有趣背景。

- TCP。IPv6支持已完全集成到最新的TCP标准中
  \[[STD7](https://www.rfc-editor.org/info/std7)\]。

- RTP完全支持IPv6
  \[[RFC3550](https://www.rfc-editor.org/info/rfc3550)\]。

- QUIC完全支持IPv6
  \[[RFC9000](https://www.rfc-editor.org/info/rfc9000)\]。

- SCTP完全支持IPv6
  \[[RFC4960](https://www.rfc-editor.org/info/rfc4960)\]。

- MPTCP完全支持IPv6
  \[[RFC8684](https://www.rfc-editor.org/info/rfc8684)\]。

此外，安全传输TLS、DTLS和SSL都可以正常使用IPv6。SIP（会话发起协议
\[[RFC3261](https://www.rfc-editor.org/info/rfc3261)\]）也是如此，在IPv6的情况下，它不需要NAT穿越支持（STUN）。

IPv4和IPv6的所有服务质量和拥塞控制考虑应该大致相同。这就是为什么
[RFC 2474](https://www.rfc-editor.org/info/rfc2474)为两个版本的IP定义相同的差异化服务，ECN（显式拥塞通知
\[[RFC3168](https://www.rfc-editor.org/info/rfc3168)\]）也是如此。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Routing.md) [<ins>下一页</ins>](Extension%20headers%20and%20options.md) [<ins>顶部</ins>](02.%20IPv6%20Basic%20Technology.md)
