## 为什么是版本 6

本节主要是历史性的。简而言之，IPv6 是在 1990 年代初期设计的，因为人们知道 IPv4 注定会耗尽地址。但为什么版本号是 6？

有些人问为什么 IPv4 跳到了版本 6，跳过了下一个数字。这与程序员的迷信无关，即奇数应该是测试版本。也许我们应该先问为什么 IPv4 是版本 4。简单来说，这是因为版本 0 到 3 在 1977 年和 1978 年期间在从 ARPANET 向 TCP/IP 演变过程中被分配了。因此版本 4 是最终设计中可用的下一个数字 [RFC 791](https://www.rfc-editor.org/info/rfc791)。已故的 Danny Cohen（参与其中的先驱之一）在视频 [IP 语音的简要史前史](https://youtu.be/av4KF1j-wp4)的 38 分 26 秒处给出了更微妙的解释。

那么为什么不是 IPv5？答案非常简单。IP 报头的版本字段中的数字 5 已经分配给了所谓的互联网流协议（Internet Stream Protocol）或 ST。这有点令人困惑，但 ST、ST-2 和 ST-2+ \[[RFC1819](https://www.rfc-editor.org/info/rfc1819)\] 被设计并提议作为需要服务质量的语音和视频等应用的协议。由于 IP 数据报是以"尽力而为"的方式传递的，ST 提议更像 ATM 网络，使用有状态关系、排队等等。每个 ST 流将保持连接状态和动态控制以确保服务质量。正如我们在 [RFC 1190](https://www.rfc-editor.org/info/rfc1190) 中看到的，ST 报头与 IPv4 完全不同，除了第一个字段是版本号 5：

```
 0                   1                   2                   3
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |  ST=5 | Ver=2 | Pri |T| Bits  |           TotalBytes          |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |              HID              |        HeaderChecksum         |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                                                               |
   +-                          Timestamp                          -+
   |                                                               |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

由于 ST 与 IP 不兼容，因此分配了下一个版本号来识别其数据包。从那时起，数字 5 就被保留用于 IP 版本字段（第 3 层）和协议号（第 4 层）字段中的 ST。这个想法是路由器可以区分数据包，或者 IPv4 数据包可以携带封装的 ST 数据包，其中数字 5 将显示为上层协议。从 [RFC 762](https://www.rfc-editor.org/info/rfc762) 开始，我们可以在"协议号"中看到分配的数字 5：

```
                 ASSIGNED INTERNET PROTOCOL NUMBERS

   In the Internet Protocol (IP) [44] there is a field to identify the
   the next level protocol.  This field is 8 bits in size.  This field
   is called Protocol in the IP header.

   Assigned Internet Protocol Numbers

      Decimal    Octal      Protocol Numbers                  References
      -------    -----      ----------------                  ----------
           0       0         Reserved
           1       1         raw internet datagrams                 [44]
           2       2         TCP-3                                  [36]
           3       3         Gateway-to-Gateway                     [49]
           4       4         Gateway Monitoring Message             [41]
           5       5         ST                                     [45]
           6       6         TCP-4                                  [46]
```

ST 协议从未离开实验阶段，但为了在早期互联网上进行实时实验，需要其自己的版本号。虽然（据我们所知）今天互联网上任何地方都没有使用 ST，但其版本号仍然被分配，因此__下一代 IP__ 使用该数字是没有意义的，因此它被"跳过"了。数字 6 仅在几年后的"已分配号码"更新 \[[RFC1700](https://www.rfc-editor.org/info/rfc1700)\] 中出现，当时被命名为"简单互联网协议"（Simple Internet Protocol，SIP）。这个缩写已被会话发起协议（Session Initiation Protocol）重用。

```
Assigned Internet Version Numbers

Decimal   Keyword    Version                            References
-------   -------    -------                            ----------
    0                Reserved                                [JBP]
  1-3                Unassigned                              [JBP]
    4       IP       Internet Protocol                [RFC791,JBP]
    5       ST       ST Datagram Mode                [RFC1190,JWF]
    6       SIP      Simple Internet Protocol                [RH6]
    7       TP/IX    TP/IX: The Next Internet                [RXU]
    8       PIP      The P Internet Protocol                 [PXF]
    9       TUBA     TUBA                                    [RXC]
10-14                Unassigned                              [JBP]
   15                Reserved                                [JBP]
```

请注意，IANA 为后来成为 IPv6 的"竞争者"分配了数字 6 到 9。数字 7 被选择用于 TP/IX \[[RFC1475](https://www.rfc-editor.org/info/rfc1475)\]，因为其设计者预期 ST 版本 2 将使用数字 6，但这并没有发生。但出乎意料的是，1992 年 6 月在日本神户举行的互联网协会 INET 会议期间，IAB 成员宣布了一个不同的"IPv7"提案。当时 IETF 工程师对新协议没有达成共识，一些 IAB 成员提议使用 ISO/OSI 的 CLNP——在没有正式 IANA 分配的情况下将其指定为 IPv7。这在互联网社区引起了一些不适，在技术圈子中被称为"神户事件"。数字 8 和 9 被用于最终合并到 IPv6 最终设计中的提案。作为 4 之后的最低可用数字，并且已经被同一作者的 SIP 使用，数字 6 在 [RFC 1883](https://www.rfc-editor.org/info/rfc1883) 的第一个正式规范中被保留下来。因此，不要期待未来会有 IP 版本 7 或 8，甚至也不会有版本 9，它也属于愚人节玩笑 \[[RFC1606](https://www.rfc-editor.org/info/rfc1606)\]。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Acknowledgments.md) [<ins>下一页</ins>](../02.%20IPv6%20Basic%20Technology/02.%20IPv6%20Basic%20Technology.md) [<ins>返回顶部</ins>](01.%20Introduction%20and%20Foreword.md)
