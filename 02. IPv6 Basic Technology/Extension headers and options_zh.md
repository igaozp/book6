## 扩展头和选项

如
[2. 数据包格式](../02.%20IPv6%20Basic%20Technology/Packet%20Format.md)中所述，
每个IPv6数据包可以在传输层有效载荷（UDP、TCP等）之前包含一个或多个扩展头。有关扩展头和选项如何编码的精确规则，请参见
[STD 86](https://www.rfc-editor.org/info/std86)。当前标准化的扩展头集在
[IANA](https://www.iana.org/assignments/ipv6-parameters/ipv6-parameters.xhtml#extension-header)上列出。
以下是关于最常见扩展头的一些注释：

- 逐跳（HBH）选项，用于应由路径上每个节点检查的数据包级选项。定义的选项及其参考文献在
  [IANA](https://www.iana.org/assignments/ipv6-parameters/ipv6-parameters.xhtml#ipv6-parameters-2)上列出。
  选项0x05"路由器警告"可能是最有趣的；它旨在警告路径上的每个路由器，数据包可能需要特殊处理。路由器警告类型在
  [IANA](https://www.iana.org/assignments/ipv6-routeralert-values/ipv6-routeralert-values.xhtml)有自己的注册表。
  不幸的是，经验表明HBH头可能存在问题，许多路由器实际上并不处理它。因此，路由器警告已被弃用于未来的协议
  \[[RFC 9805](https://www.rfc-editor.org/info/rfc9805)\]。

  更一般地说，
  [RFC 8200](https://www.rfc-editor.org/info/rfc8200)指出"现在期望沿数据包传递路径的节点仅在明确配置时才检查和处理逐跳选项头。"此问题的一些缓解措施在
  [RFC 9673](https://www.rfc-editor.org/info/rfc9673)中描述。

- 分片头，当数据包已被分片时（仅在源端发生，如果原始数据包超过传输路径的已知MTU，至少为IPv6的最小MTU 1280字节）。IPv6分片与IPv4分片显著不同，后者可能在路径的任何地方发生。技术细节在
  [STD 86](https://www.rfc-editor.org/info/std86)中描述。当然，分片与PMTUD（路径最大传输单元确定）相互作用，因此懒惰的解决方案是永远不超过1280字节的限制。对于PMTUD，请参见[STD 87](https://www.rfc-editor.org/info/std87)、
  [RFC 8899](https://www.rfc-editor.org/info/rfc8899)和（恐怖故事）[RFC 7690](https://www.rfc-editor.org/info/rfc7690)。另请参见"IP分片被认为是脆弱的"以获取操作建议
  \[[BCP230](https://www.rfc-editor.org/info/bcp230)\]。

- 目标选项，用于仅在目标节点有用的数据包级选项。这些也在
  [IANA](https://www.iana.org/assignments/ipv6-parameters/ipv6-parameters.xhtml#ipv6-parameters-2)上列出。

- 路由头，如果需要非标准路由。有各种
  [路由头类型](https://www.iana.org/assignments/ipv6-parameters/ipv6-parameters.xhtml#ipv6-parameters-2)。
  当前一个重要的是段路由头（类型4，
  [RFC 8754](https://www.rfc-editor.org/info/rfc8754)）。充当中间目的地并因此处理路由头的路由器在
  [STD 86](https://www.rfc-editor.org/info/std86)中被称为"中间节点"。

- 封装安全有效载荷，如果使用
  [IPsec](https://www.rfc-editor.org/info/rfc4303)。这是IPv6第3层安全的定义机制。这可能是使用最广泛的IPv6扩展头。

逐跳和目标选项都在选项类型中包含标志位，用于可能不理解该选项的节点，告诉节点是简单地忽略未知选项，还是丢弃整个数据包并可能发送ICMP响应。

IPv6扩展头存在一个公认的运营问题：虽然它们在具有一致管理和安全规则的有限域内运行良好，但它们无法可靠地跨开放互联网传输，可能是由于防火墙和路由器过滤规则。[RFC 7872](https://www.rfc-editor.org/info/rfc7872)报告了2015年的情况，并且正在进行更新类似测量的工作。运营影响在
[RFC 9098](https://www.rfc-editor.org/info/rfc9098)中描述，过滤建议在
[RFC 9288](https://www.rfc-editor.org/info/rfc9288)中。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Transport%20protocols.md) [<ins>下一页</ins>](Traffic%20class%20and%20flow%20label.md) [<ins>顶部</ins>](02.%20IPv6%20Basic%20Technology.md)
