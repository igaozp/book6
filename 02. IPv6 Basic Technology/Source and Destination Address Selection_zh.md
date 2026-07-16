## 源地址和目标地址选择

如
\[[2. 地址](../02.%20IPv6%20Basic%20Technology/Addresses.md)\]中所述，主机每个接口将有多个IPv6地址。由于同一地址族中存在多个地址，因此必须有一个过程来选择一般使用的源地址和目标地址对。此地址选择在
[RFC 6724](https://www.rfc-editor.org/info/rfc6724)中描述，此外，更复杂的主题和场景可以在
\[[6. 多前缀操作](../06.%20Management%20and%20Operations/Multi-prefix%20operation.md)\]
部分找到。地址选择由IPv6的多地址特性所提供的灵活性以及给定主机和应用程序进一步定义行为的能力而变得复杂。服务器应用程序是规定性地定义特定地址以用于源流量的应用程序的最佳示例。在应用程序指定特定地址的情况下，该特定流量的过程通常就在那里停止，主机不需要进一步评估，所讨论的流量从给定应用程序指定的地址发出。

在给定应用程序没有特异性的情况下，操作系统将评估IPv4和IPv6地址族的可用地址，并根据一组规则对它们进行排序，根据源地址和目标地址对（为了文档和简洁，通常缩写为"SA/DA"）从其评估列表中返回顶部地址。排序按顺序进行，一旦匹配就停止。给定流量的地址对按以下顺序评估：

1. 优先相同地址联系
1. 优先适当的地址范围
1. 避免弃用的地址
1. 优先家庭地址
1. 优先传出接口
1. 优先匹配地址标签
1. 优先隐私地址
1. 使用最长匹配前缀

默认排序行为通常由以下表定义：

```
Prefix                            Prec   Label
::1/128                           50     0
::/0                              40     1
::ffff:0.0.0.0/96                 35     4
2002::/16                         30     2
2001::/32                          5     5
fc00::/7                           3    13
::/96                              1     3
fec0::/16                          1    11
3ffe::/16                          1    12
```

### 目标地址选择

目标地址选择有些复杂，应该理解它是可配置的，并且可能基于给定IPv6网络堆栈的实现和操作系统的年龄而有所不一致。在撰写本文时，仍有一些操作系统采用
[RFC 3484](https://www.rfc-editor.org/info/rfc3484)的某些方面或完整实现，该RFC于2012年被[RFC 6724](https://www.rfc-editor.org/info/rfc6724)废弃。要完全理解地址选择，可以参考现代Linux系统中的_/etc/gai.conf_文件，因为它有管理该过程的规则的最简洁示例。

### 更改地址选择策略

在绝大多数用例中，默认策略表是不变和一致的。但是，在Linux和Microsoft Windows等平台上，可以调整此表以创建所需的行为，包括创建地址配对、调整首选项和唯一的流量SA/DA特征。

使用DHCPv6选项84和85的站点可以通过
[RFC 7078](https://www.rfc-editor.org/info/rfc7078)更改地址选择的默认设置，但不幸的是这并未被广泛实现。原则上，这也可以通过每个主机中的系统命令实现（例如，Windows中的_netsh interface ipv6 add prefixpolicy_和Linux中的_ip addrlabel add prefix_），但这很少做到。结果是主机通常应用其操作系统版本的默认策略，即使不同的策略会更好地工作。

### ULA注意事项

在IPv4和ULA都存在的默认情况下，IPv4将是首选协议。这通常与人们对IPv6行为在双栈环境中如何工作的一般理解相反，可以在前面提到的_gai.conf_文件中通过以下行观察到：

```
Prefix                            Prec   Label
...
::ffff:0.0.0.0/96                 35     4
```

这是IPv4地址空间的IPv6转换。因为这个地址块的首选项值高于ULA地址，所以它将由操作系统和应用程序默认首选，因为它的首选项值。

[draft-ietf-v6ops-ula](https://datatracker.ietf.org/doc/draft-ietf-v6ops-ula/)
详细描述了使用ULA的许多注意事项，特别是在双栈环境中。应该注意的是，在纯IPv6环境中，地址选择过程通常没有问题，利用上述过程。

### 标签

不要与流标签混淆，地址标签是选择过程中一个强大且经常被忽视的工具。地址标签允许前缀或地址配对，从而强制流量对以一致或期望的方式行事，这可能因技术、安全或策略原因而与默认不同。采用基本的Linux系统并创建具有匹配标签的地址对将导致系统根据标签行事，并根据运营商确定的SA/DA对生成流量。

使用原始的Linux系统，可以使用ip命令`{ip addrlabel add prefix <PREFIX> label <LABEL>}`轻松创建工作的SA/DA对进行以下更改。

例如：

```
sudo ip addrlabel add prefix fd68:1e02:dc1a:9:ba27:ebff:fe84:781c/128 label 97
sudo ip addrlabel add prefix 2001:db8:4009:81c::200e/128 label 97
```

产生：

```
user@v6host:~$ sudo ip addrlabel list
prefix 2001:db8:4009:81c::200e/128 label 97
prefix fd68:1e02:dc1a:9:ba27:ebff:fe84:781c/128 label 97
prefix ::1/128 label 0
prefix ::/96 label 3
prefix ::ffff:0.0.0.0/96 label 4
prefix 2001::/32 label 6
prefix 2001:10::/28 label 7
prefix 3ffe::/16 label 12
prefix 2002::/16 label 2
prefix fec0::/10 label 11
prefix fc00::/7 label 5
prefix ::/0 label 1
```

### 源地址选择

在实践中，除了链路本地、GUA和ULA默认首选项之外，源地址选择很难配置，并且因主机和应用程序实现而异。但是，可以使用IPv6地址标签机制创建地址配对。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](Traffic%20class%20and%20flow%20label.md) [<ins>下一页</ins>](../03.%20Coexistence%20with%20Legacy%20IPv4/03.%20Coexistence%20with%20Legacy%20IPv4.md) [<ins>顶部</ins>](02.%20IPv6%20Basic%20Technology.md)
