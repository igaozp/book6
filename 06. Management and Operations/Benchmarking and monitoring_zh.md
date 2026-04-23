## 基准测试与监控

今天，IPv6监控经常被遗忘、忽视或从错误的角度进行监控。

一些经验实例：

- 大型企业网络没有IPv6监控，因为监控系统所在的网络部分没有IPv6。

- 具有AAAA记录
  \[[2. DNS](../02.%20IPv6%20Basic%20Technology/DNS.md)\]和适当配置的Web服务；监控表明一切正常，但用户无法通过IPv6从互联网访问Web服务。有人忘记了防火墙规则，而监控系统在网络内部。

- 具有AAAA记录的邮件（SMTP）服务器。但是，由于某种原因，IPv6被禁用（或被防火墙阻止），但没有人删除AAAA记录。内部没有注意到，即他们没有通过IPv6进行监控。

监控IPv4或IPv6服务之间没有根本区别；只是必须对所有服务进行监控，如果它们是双栈的，则对两个协议都要进行监控。

在上述邮件服务器示例中，可能涉及三个不同的团队，他们要么没有相互沟通，要么实施了不充分的流程且没有自动化。

与此相关，实施IPv6也为运营商提供了清理运维文档、运维基础设施和NOC流程的机会。这也可能是实施更多自动化的机会。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Remote%20configuration.md) [<ins>下一页</ins>](Routing%20operation.md) [<ins>返回顶部</ins>](06.%20Management%20and%20Operations.md)
