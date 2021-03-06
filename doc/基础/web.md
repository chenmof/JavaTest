# 概念

##MVC

MVC本来是存在于Desktop程序中的，M是指数据模型，V是指用户界面，C则是控制器。使用MVC的目的是将M和V的实现代码分离，从而使同一个程序可以使用不同的表现形式。

##"GET方式提交的数据最多只能是1024字节"?  错

因为GET是通过URL提交数据，那么GET可提交的数据量就跟URL的长度有直接关系了。而实际上，URL不存在参数上限的问题，HTTP协议规范没有对URL长度进行限制。这个限制是特定的浏览器及服务器对它的限制。IE对URL长度的限制是2083字节(2K+35)。对于其他浏览器，如Netscape、FireFox等，理论上没有长度限制，其限制取决于操作系统的支持。

Get是向服务器发索取数据的一种请求，而Post是向服务器提交数据的一种请求，在FORM（表单）中，Method默认为"GET"，实质上，GET和POST只是发送机制不同，并不是一个取一个发！

##GET & POST

GET请求会被浏览器主动cache，而POST不会，除非手动设置。 GET请求只能进行url编码，而POST支持多种编码方式。 GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留。 GET请求在URL中传送的参数是有长度限制的，而POST么有。 对参数的数据类型，GET只接受ASCII字符，而POST没有限制。 GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息。 GET参数通过URL传递，POST放在Request body中。

GET和POST是什么?HTTP协议中的两种发送请求的方法。
HTTP的底层是TCP/IP。所以GET和POST的底层也是TCP/IP，也就是说，GET/POST都是TCP链接。GET和POST能做的事情是一样一样的。你要给GET加上request body，给POST带上url参数，技术上是完全行的通的。


##GET & POST 重大区别

GET产生一个TCP数据包;POST产生两个TCP数据包。

对于GET方式的请求，浏览器会把http header和data一并发送出去，服务器响应200(返回数据);
而对于POST，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 ok(返回数据)。

也就是说，GET只需要汽车跑一趟就把货送到了，而POST得跑两趟，第一趟，先去和服务器打个招呼“嗨，我等下要送一批货来，你们打开门迎接我”，然后再回头把货送过去。

1. GET与POST都有自己的语义，不能随便混用。
2. 据研究，在网络环境好的情况下，发一次包的时间和发两次包的时间差别基本可以无视。而在网络环境差的情况下，两次包的TCP在验证数据包完整性上，有非常大的优点。
3. 并不是所有浏览器都会在POST中发送两次包，Firefox就只发送一次。

##PUT

在HTTP中，PUT被定义为idempotent的方法，POST则不是，这是一个很重要的区别。

PUT操作是幂等的。所谓幂等是指不管进行多少次操作，结果都一样。比如我用PUT修改一篇文章，然后在做同样的操作，每次操作后的结果并没有不同

##汽车TCP

在我大万维网世界中，TCP就像汽车，我们用TCP来运输数据，它很可靠，从来不会发生丢件少件的现象。

##交通规则HTTP 

HTTP给汽车运输设定了好几个服务类别，有GET, POST, PUT, DELETE等等，HTTP规定，当执行GET请求的时候，要给汽车贴上GET的标签(设置method为GET)，而且要求把传送的数据放在车顶上(url中)以方便记录。如果是POST请求，就要在车上贴上POST的标签，并把货物放在车厢里。当然，你也可以在GET的时候往车厢内偷偷藏点货物，但是这是很不光彩;也可以在POST的时候在车顶上也放一些数据，让人觉得傻乎乎的。HTTP只是个行为准则，而TCP才是GET和POST怎么实现的基本。

##运输公司 浏览器

不同的浏览器(发起http请求)和服务器(接受http请求)就是不同的运输公司。

虽然理论上，你可以在车顶上无限的堆货物(url中无限加参数)。但是运输公司可不傻，装货和卸货也是有很大成本的，他们会限制单次运输量来控制风险，数据量太大对浏览器和服务器都是很大负担。业界不成文的规定是，(大多数)浏览器通常都会限制url长度在2K个字节，而(大多数)服务器最多处理64K大小的url。超过的部分，恕不处理。如果你用GET服务，在request body偷偷藏了数据，不同服务器的处理方式也是不同的，有些服务器会帮你卸货，读出数据，有些服务器直接忽略，所以，虽然GET可以带request body，也不能保证一定能被接收到哦。

##Https

HTTPS（全称：Hypertext Transfer Protocol over Secure Socket Layer），是以安全为目标的HTTP通道，简单讲是HTTP的安全版。即HTTP下加入SSL层，HTTPS的安全基础是SSL，因此加密的详细内容就需要SSL。


超文本传输协议 (HTTP-Hypertext transfer protocol) 是一种详细规定了浏览器和万维网服务器之间互相通信的规则，通过因特网传送万维网文档的数据传送协议。


##http和https区别

https协议需要到ca申请证书，一般免费证书很少，需要交费。http是超文本传输协议，信息是明文传输，https 则是具有安全性的ssl加密传输协议http和https使用的是完全不同的连接方式用的端口也不一样,前者是80,后者是443。http的连接很简单,是无状态的HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、

http的连接很简单,是无状态的。HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议 要比http协议安全



### 为什么用了 HTTPS 就是安全的？

### HTTPS 的底层原理如何实现？

### 用了 HTTPS 就一定安全吗？

大家可能都听说过 HTTPS 协议之所以是安全的是因为 HTTPS 协议会对传输的数据进行加密，而加密过程是使用了**非对称加密实现**。但其实，**HTTPS 在内容传输的加密上使用的是对称加密，非对称加密只作用在证书验证阶段**。

HTTPS 的整体过程分为证书验证和数据传输阶段，

证书验证阶段：

- 浏览器发起 HTTPS 请求。
- 服务端返回 HTTPS 证书。
- 客户端验证证书是否合法，如果不合法则提示告警。

数据传输阶段：

- 当证书验证合法后，在本地生成随机数。
- 通过公钥加密随机数，并把加密后的随机数传输到服务端。
- 服务端通过私钥对随机数进行解密。
- 服务端通过客户端传入的随机数构造对称加密算法，对返回结果内容进行加密后传输。

### 为什么数据传输是用对称加密？

首先，非对称加密的加解密效率是非常低的，而 HTTP 的应用场景中通常端与端之间存在大量的交互，非对称加密的效率是无法接受的。

另外，在 HTTPS 的场景中只有服务端保存了私钥，一对公私钥只能实现单向的加解密，所以 HTTPS 中内容传输加密采取的是对称加密，而不是非对称加密。