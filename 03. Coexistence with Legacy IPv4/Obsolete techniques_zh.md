## 过时的技术

随着 IPv6 的成熟和人们获得运营经验，各种共存和过渡技术要么被证明不令人满意，要么只是被事件所取代。本节仅列出此类技术，并提供最少的解释。建议读者在新部署中忽略这些技术，并考虑从现有部署中删除它们。

通过 IPv4 隧道传输 IPv6，或相反，仍然是共存的基础，尽管各种特定的隧道机制在下面被列为过时。

请注意，三种此类机制（6to4、Teredo 和 ISATAP）在它们身后留下了一些与 IPv4 协议类型 41 相关的操作安全风险，如
[Plight at the End of the Tunnel - Legacy IPv6 Transition Mechanisms in the Wild](https://doi.org/10.1007/978-3-030-72582-2_23) 中所述，
预印本 [在这里](https://dataplane.org/jtk/publications/kgkp-pam-21.pdf)。

- 在没有显式隧道的 IPv4 域上传输 IPv6
  \[[RFC2529](https://www.rfc-editor.org/info/rfc2529)\]。据所知，这从未在实践中部署过。

- IPv6 隧道代理
  \[[RFC3053](https://www.rfc-editor.org/info/rfc3053)\]。

- 通过 IPv4 云连接 IPv6 域（"6to4"）
  \[[RFC3056](https://www.rfc-editor.org/info/rfc3056)\]
  \[[RFC3068](https://www.rfc-editor.org/info/rfc3068)\]。这方面的问题记录在
  [RFC 6343](https://www.rfc-editor.org/info/rfc6343) 中，它在很大程度上被 [RFC 7526](https://www.rfc-editor.org/info/rfc7526) 弃用。

- Teredo：通过网络地址转换 (NAT) 在 UDP 上隧道传输 IPv6
  \[[RFC4380](https://www.rfc-editor.org/info/rfc4380)\]。

- 基于 SOCKS 的 IPv6/IPv4 网关
  \[[RFC3089](https://www.rfc-editor.org/info/rfc3089)\]。

- ISATAP \[[RFC5214](https://www.rfc-editor.org/info/rfc5214)\]。

- 6rd \[[RFC5569](https://www.rfc-editor.org/info/rfc5569)\]。

- 用于 IPv6 过渡的增量运营商级 NAT (CGN)
  \[[RFC6264](https://www.rfc-editor.org/info/rfc6264)\]。

- 6a44 \[[RFC6751](https://www.rfc-editor.org/info/rfc6751)\]。

- 在 NAT64 的上下文中，
  [RFC 7050](https://www.rfc-editor.org/info/rfc7050) 不应再使用。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Translation%20and%20IPv4%20as%20a%20service.md) [<ins>下一页</ins>](IPv6%20primary%20differences%20from%20IPv4.md) [<ins>顶部</ins>](03.%20Coexistence%20with%20Legacy%20IPv4.md)
