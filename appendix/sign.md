# 服务端 HTTP 交互及请求签名

本节介绍平台服务端和商店/游戏服务端之间的 HTTP 交互约定及 HTTP 请求合法性签名计算方法。

> 我们提供了 Java, PHP 和 JavaScript 签名算法参考实现。

[阿里电视游戏开放平台](http://open.aliplay.com)会为每一个游戏分配一个凭据，包含 `AppKey`, `AppSecret` 和 `BaodianSecret` 三项。但本节的签名算法，只使用 `AppKey` 和 `BaodianSecret` 。

> 务必妥善传递和存放 `AppSecret` 和 `BaodianSecret` ，避免泄漏。

约定用 HTTP GET 方法来发送请求，在 HTTP 响应体中用 json 格式返回结果。请求接收方应实现幂等操作，也就是说，同一语义的多次请求，效果不能叠加。请参考[幂等性](http://zh.wikipedia.org/wiki/%E5%86%AA%E7%AD%89)（ [Idempotence](http://en.wikipedia.org/wiki/Idempotence) ）。

HTTP 请求必须带一个 `sign` 参数，其值按如下计算方法产生。对于一组 `(key1, value1)`, `(key2, value2)`, ... 和本游戏的 `BaodianSecret` ：

1. 将参数按 key 的[**字典序**](http://en.wikipedia.org/wiki/Alphabetical_order)（也称为“字母表顺序”）排列，组成形如 `key1value1key2value2...BaodianSecret` 的字符串
2. 计算该字符串的 **GBK 编码字节序列**的 md5 校验码
> MD5 校验码计算过程的输入是字节序列，而不是字符串。在有些编程语言中，字符串是有内部编码的，如 Java 和 JavaScript 都是用 UTF-16 内码；而在另一些编程语言则没有字符串内部编码，如 PHP 。因此，在计算签名时，需要先转换成 GBK 编码字节流（ASCII 和 GBK 是兼容的，所以，纯 ASCII 字符串不必转换）。显然，这是一个设计缺陷，但还没有修订。

举例来说，参数 title 取值 “100金币”，在计算 md5 时参与计算的是 “title100金币”，更准确地说 ， 是 `74 69 74 6c 65 31 30 30 bd f0 b1 d2` 这 16 个字节，其中 `bd f0 b1 d2` 是“金币”的 GBK 编码的十六进制表示（一个汉字两个字节）。在 LANG=en_US.UTF-8 环境下，用 `echo -n title100金币 | iconv -f utf8 -t gbk` 可以获得原始字节序列。在 HTTP 请求中， 该参数是 `title=100%BD %F0%B1%D2` ，因为还需要经过 [urlencode 编码](http://www.w3.org/TR/html401/interact/forms.html?spm=0.0.0.0.pX4uQ6#h-17.13.4.1)。


