---
title: HTTP学习记录
date: 2020-09-27 10:41:52
tags:
---


## HTTP 协议方法  

方法说明支持的 |HTTP |协议版本
---|---|---
GET |获取资源|1.0、1.1
POST |传输实体主体|1.0、1.1
PUT |传输文件|1.0、1.1
HEAD |获得报文首部|1.0、1.1
DELETE |删除文件|1.0、1.1
OPTIONS |询问支持的方法|1.1
TRACE |追踪路径|1.1
CONNECT |要求用隧道协议连接代理|1.1
LINK |建立和资源之间的联系|1.0
UNLINE |断开连接关系|1.0
  
  * CONNECT 要求用隧道协议连接代理
    * CONNECT 方法要求在与代理服务器通信时建立隧道，实现用隧道协议进行 TCP 通信。主要使用SSL（Secure Sockets Layer，安全套接层）和 TLS（Transport Layer Security，传输层安全）协议把通信内容加 密后经网络隧道传输。
    * CONNECT 代理服务器名:端口号 HTTP版本
      ![在这里插入图片描述](https://img-blog.csdnimg.cn/2020092710483083.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODkyNTEx,size_16,color_FFFFFF,t_70#pic_center)

## 持久连接节省通信量
- HTTP Persistent Connections，也称为 HTTP keep-alive 或HTTP connection reuse
  - HTTP/1.1 和一部分的 HTTP/1.0
  - HTTP/1.1 中，所有的连接默认都是持久连接，但在 HTTP/1.0 内并未标准化。
- 管线化(pipelining)
  - 持久连接使得多数请求以管线化（pipelining）方式发送成为可能。从前发送请求后需等待并收到响应，才能发送下一个请求。管线化技术出现后，不**用等待响应亦可直接发送下一个请求**。

## 使用Cookie的状态管理


# 临时 杂乱

* 优质参考
  * [HTTP 面试知识点总结：秒杀90%面试考点！](https://mp.weixin.qq.com/s?__biz=MzI3ODg2OTY1OQ==&mid=2247485774&idx=1&sn=f0ff2fbf00063782da8ee1b0b08a15f7&chksm=eb512abadc26a3ac6388d58979a46540c054c17e7b6d7f3f37a99713ba47ed16d49fb8691292&mpshare=1&scene=23&srcid=0916a3vm6T5tuRlDm57jgvTd&sharer_sharetime=1601105665371&sharer_shareid=fb98e1c0050218077fbf22b2cbfe3976#rd)
  * 《图解Http》

* ARP协议
* http连接管理
  ![](https://mmbiz.qpic.cn/mmbiz_png/hkZHkS4iaqMUKaBzIGicrezVwjQWXxEkYweGksHGRjDH6kHWxibbBbTG6ic3G9WH8W13m2K0WQUiaGr2drzwSJJicibicw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
  * 长连接与短连接
  	* HTTP 1.0规定浏览器与服务器只保持短暂的连接，浏览器的每次请求都需要与服务器建立一个TCP连接，服务器完成请求处理后立即断开TCP连接，服务器不跟踪每个客户也不记录过去的请求。
  	* HTTP 1.1支持持久连接（HTTP/1.1的默认模式使用带流水线的持久连接）
  * 流水线
  	* HTTP 请求是按顺序发出的，下一个请求只有在当前请求收到响应之后才会被发出。由于受到网络延迟和带宽的限制，在下一个请求被发送到服务器之前，可能需要等待很长时间。流水线是在同一条长连接上连续发出请求，而不用等待响应返回，这样可以减少延迟。	
* **Cookie**
  	* HTTP/1.1 引入 Cookie 来保存状态信息
  	* 由于之后每次请求都会需要携带 Cookie 数据，因此会带来额外的性能开销（尤其是在移动环境下）。
  	* 但现在随着现代浏览器开始支持各种各样的存储方式，Cookie 渐渐被淘汰。新的浏览器 API 已经允许开发者直接将数据存储到本地，如使用 Web storage API（本地存储和会话存储）或 IndexedDB。
  	* 用途
      	* 会话状态管理（如用户登录状态、购物车、游戏分数或其它需要记录的信息）
      	* 个性化设置（如用户自定义设置、主题等）
      	* 浏览器行为跟踪（如跟踪分析用户行为等）
  	* 分类
    	* 会话期Cookie:浏览器关闭之后它会被自动删除，也就是说它仅在会话期内有效。
    	* 持久性Cookie:指定过期时间（Expires）或有效期（max-age）之后就成为了持久性的 Cookie。
  	* 作用域
    	* Domain 标识指定了哪些主机可以接受 Cookie。如果不指定，默认为当前文档的主机（不包含子域名）。如果指定了 Domain，则一般包含子域名。例如，如果设置 Domain=mozilla.org，则 Cookie 也包含在子域名中（如 developer.mozilla.org）。
    	* Path 标识指定了主机下的哪些路径可以接受 Cookie（该 URL 路径必须存在于请求 URL 中）。以字符 %x2F ("/") 作为路径分隔符，子路径也会被匹配。例如，设置 Path=/docs，则以下地址都会匹配：/docs /docs/Web/  /docs/Web/HTTP
  	* HttpOnly
    	* 标记为 HttpOnly 的 Cookie 不能被 JavaScript 脚本调用。跨站脚本攻击 (XSS) 常常使用 JavaScript 的 document.cookie API 窃取用户的 Cookie 信息，因此使用 HttpOnly 标记可以在一定程度上避免 XSS 攻击。
  	* Secure(??)
    	* 标记为 Secure 的 Cookie 只能通过被 HTTPS 协议加密过的请求发送给服务端。但即便设置了 Secure 标记，敏感信息也不应该通过 Cookie 传输，因为 Cookie 有其固有的不安全性，Secure 标记也无法提供确实的安全保障。

* **Session**
  * 除了可以将用户信息通过 Cookie 存储在用户浏览器中，也可以利用 Session 存储在服务器端，存储在服务器端的信息更加安全。
  * Session 可以存储在服务器上的文件、数据库或者内存中。也可以将 Session 存储在 Redis 这种内存型数据库中，效率会更高。
  * 使用 Session 维护用户登录状态的过程如下：
    * 用户进行登录时，用户提交包含用户名和密码的表单，放入 HTTP 请求报文中；
    * 服务器验证该用户名和密码，如果正确则把用户信息存储到 Redis 中，它在 Redis 中的 Key 称为 Session ID；
    * 服务器返回的响应报文的 Set-Cookie 首部字段包含了这个 Session ID，客户端收到响应报文之后将该 Cookie 值存入浏览器中；
    * 客户端之后对同一个服务器进行请求时会包含该 Cookie 值，服务器收到之后提取出 Session ID，从 Redis 中取出用户信息，继续之前的业务操作。
  * 应该注意 Session ID 的安全性问题，不能让它被恶意攻击者轻易获取，那么就不能产生一个容易被猜到的 Session ID 值。此外，还需要经常重新生成 Session ID。在对安全性要求极高的场景下，例如转账等操作，除了使用 Session 管理用户状态之外，还需要对用户进行重新验证，比如重新输入密码，或者使用短信验证码等方式。
* 浏览器禁用Session
  * 此时无法使用 Cookie 来保存用户信息，只能使用 Session。除此之外，不能再将 Session ID 存放到 Cookie 中，而是使用 URL 重写技术，将 Session ID 作为 URL 的参数进行传递。
* Cookie和Session
  * Cookie 只能存储 ASCII 码字符串，而 Session 则可以存储任何类型的数据，因此在考虑数据复杂性时首选 Session；
  * Cookie 存储在浏览器中，容易被恶意查看。如果非要将一些隐私数据存在 Cookie 中，可以将 Cookie 值进行加密，然后在服务器进行解密；
  * 对于大型网站，如果用户所有的信息都存储在 Session 中，那么开销是非常大的，因此不建议将所有的用户信息都存储到 Session 中。

* 缓存（？？）
* 内容协商
* 内容编码
* 范围请求

* 虚拟主机
  * HTTP/1.1 使用虚拟主机技术，使得一台服务器拥有多个域名，并且在逻辑上可以看成多个服务器。
* 通信数据转发
  * 代理
    * 代理服务器接受客户端的请求，并且转发给其它服务器。
    * 使用代理的主要目的是：
      * 缓存
      * 负载均衡
      * 网络访问控制
      * 访问日志记录
    * 分类
      * 正向代理
      * 反向代理
  
  
  * 网关
    * 与代理服务器不同的是，网关服务器会将 HTTP 转化为其它协议进行通信，从而请求其它非 HTTP 服务器的服务。
  * 隧道
    * 使用 SSL 等加密手段，在客户端和服务器之间建立一条安全的通信线路。

* HTTPS
  * HTTP的安全性问题
    * 使用明文进行通信，内容可能会被窃听
    * 不验证通信方的身份，通信方的身份有可能遭遇伪装
    * 无法证明报文的完整性，报文有可能遭篡改
  * HTTPS： HTTP先和SSL(Secure Sockets Layer)通信，在由SSL和TCP通信，HTTPS使用了隧道进行通信，通过使用SSL,HTTPS具有了**加密（防窃听），认证（防伪装）和完整性保护（反篡改）**（怎么实现的？？）
![](https://mmbiz.qpic.cn/mmbiz_jpg/hkZHkS4iaqMUKaBzIGicrezVwjQWXxEkYwsXMMnmhMyymswJ1q0whCIjt5rrn95X80sgn796z4NtibmzCh4Diaiarow/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
  * 加密
    * 对称密钥加密（Symmetric-Key Encryption）,加密和解密使用同一密钥
      * 优点：运算速度快
      * 缺点：无法安全地蒋密钥传输给通信方
![](https://mmbiz.qpic.cn/mmbiz_png/hkZHkS4iaqMUKaBzIGicrezVwjQWXxEkYwTfaxdWwSajkvDwyC2vTDRKIX622KqqFkQ2NqwDzj9AJEMRIGibMdXIQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
    * **非对称加密**
      * 又称公开密钥加密（Public-Key Encryption）加密和解密使用不同的密钥
      * 公开密钥所有人都可以获得，通信发送方获得接收方的公开密钥之后，就可以使用公开密钥进行加密，接收方收到通信内容后使用私有密钥解密。
      * 非对称密钥处理可以用来加密，还可以用来进行签名（将加密的接收发送方反过来？？），因为私有密钥无法被其他人获取，因此通信发送方使用其私有密钥进行签名，通信接收方使用发送方的公开密钥进行解密，就能判断这个签名是否正确。
      * 优缺点
        * 优点：可以更安全地将公开密钥传输给通信发送方
        * 缺点：运算速度慢
	![](https://mmbiz.qpic.cn/mmbiz_png/hkZHkS4iaqMUKaBzIGicrezVwjQWXxEkYwETJZZVlibKorZZdibEgZmQSIIoVb3VtCQ3ok8WuE4c26icZdytL5pPyibw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
  * HTTPS采用的加密方式
    * HTTPS采用混合的加密机制，使用**非对称**密钥加密用于**传输对称密钥**来保证传输过程中的安全性，之后使用对称密钥加密进行通信来保证通信过程的效率。
![](https://mmbiz.qpic.cn/mmbiz_png/hkZHkS4iaqMUKaBzIGicrezVwjQWXxEkYwsK86T8lov3mj64JBRUHyc0wWM6NxjuLiaHd9r11rqIZBap2MS2rhMfw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)  

* URI(Uniform Resource Identifier)与URL(Uniform Resource Locator)
  * ![](https://mmbiz.qpic.cn/mmbiz_png/hkZHkS4iaqMUKaBzIGicrezVwjQWXxEkYwOLNJYGgzbNhLQtibibicTUbXBwdqB4YWt0Wl1HlnqibCw1VqdR9eLKMEkw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
  * URI 就是由某个协议方案表示的资源的定位标识符。协议方案是指访问资源所使用的协议类型名称。
  * URI 用字符串标识某一互联网资源，而 URL 表示资源的地点（互联网上所处的位置）。可见 **URL 是 URI 的子集**。
  * URI的格式
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200925205630138.png#pic_center)
  	* 协议方案名： 除了协议（http,ftp）,也可以使用data: 或 javascript: 这类指定数据或脚本程序的方案名
  	* 登录信息（可选项）
  	* 服务器地址：使用绝对 URI 必须指定待访问的服务器地址。地址可以是类似hackr.jp 这种 DNS 可解析的名称，或是 192.168.1.1 这类 IPv4 地址名，还可以是 [0:0:0:0:0:0:0:1] 这样用方括号括起来的 IPv6 地址名。
  	* 服务器端口号：默认80
  	* 带层次的文件路径
  	* 查询字符串
  	* 片段标识符：使用片段标识符通常可标记出已获取资源中的子资源（文档内的某个位置）。但在 RFC 中并没有明确规定其使用方法。该项也为可选项。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200927102729561.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODkyNTEx,size_16,color_FFFFFF,t_70#pic_center)

