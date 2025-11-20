## 应用程序开发者眼中的 IPv6

在一个非常理论化的世界中，应用程序开发者可以依赖 DNS 查询来返回远程主机的最佳（且唯一）地址，然后可以直接将该地址传递给网络套接字接口，而无需进一步处理。不幸的是，现实世界并非如此简单。即使不考虑版本号，也有几种类型的 IP 地址，DNS 查询可能返回各种地址。在大多数情况下，应用程序将使用 `getaddrinfo()` 函数（"获取地址信息"）来获取有效地址列表，通常包含 IPv6 和 IPv4 地址。哪一个是最佳选择，程序是否应该尝试多个地址？

我们不会详细讨论这个主题，因为本书主要不是针对应用程序开发者的。但是，运营人员需要了解，大多数应用程序的默认行为只是使用 `getaddrinfo()` 返回的*第一个*地址。一些应用程序（如 Web 浏览器）可能使用称为"happy eyeballs"的更智能方法（[RFC 8305](https://www.rfc-editor.org/info/rfc8305)），通过启发式方法检测哪个地址提供最快的响应。但是，运营人员需要了解各种地址类型，以便优化配置系统，包括每个主机中的 `getaddrinfo()` 优先级表（[RFC 6724](https://www.rfc-editor.org/info/rfc6724)）。

在开发支持 IPv6 的应用程序时，请记住 IPv6 地址比 IPv4 地址更长且外观不同。这听起来可能很明显，但过去的经验表明，这是两个最常见的问题，尤其是当您将 IPv6 地址存储在数据库中或应用程序中现有的输入字段太小时。此外，用于验证 IP 地址的正则表达式也是不同的。正如您将在本书后面了解到的，IPv6 地址有不同的类型，并且有多种编写方式。确保您的应用程序只接受正确类型的地址，也不要过于严格，只接受一种格式。用户希望使用复制粘贴或自动化，IP 地址的输入格式可能并不总是您的应用程序所期望的。始终记住："对自己做的事情保守，对接受他人的事情宽容"。使用您选择的编程语言提供的库函数可能总是一个好主意，而不是重新发明轮子，例如 Python 的 `ipaddress` 模块。并且请不要在代码中硬编码任何类型的 IP 地址。始终使其可配置，如果可能，使用 FQDN（DNS 名称）而不是 IP 地址。

地址类型在[2. 地址](../02.%20IPv6%20Basic%20Technology/Addresses.md)中进一步讨论。地址*选择*在[此处](../02.%20IPv6%20Basic%20Technology/Source%20and%20Destination%20Address%20Selection.md)讨论。应用程序如何处理 IPv4 和 IPv6 地址的混合也在[3. 双栈场景](../03.%20Coexistence%20with%20Legacy%20IPv4/Dual%20stack%20scenarios.md)中讨论。

<!-- Link lines generated automatically; do not delete -->

### [<ins>上一页</ins>](How%20a%20user%20sees%20IPv6.md) [<ins>下一页</ins>](How%20a%20network%20operations%20center%20sees%20IPv6.md) [<ins>返回顶部</ins>](01.%20Introduction%20and%20Foreword.md)
