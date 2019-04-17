尽管go是一门静态类型语言，但用户可以通过它的接口机制对行为进行描述，以此来实现动态类型匹配（dynamic typing)。

go语言的函数可以接受接口作为参数，这意味着用户只要实现了接口所需的方法，就可以在继续使用现有代码的同时向系统中引入新的代码。

与此同时，因为go语言的所有类型都实现了空接口，所以用户只需要创建出一个接受空接口作为参数的函数，就可以把任何类型的值用作该函数的实际参数。

此外，go语言还实现了一些在函数式编程中非常常见的特性，其中包括函数类型，使用函数作为值以及闭包，这些特性允许用户使用已有的函数来构建新的函数，从而帮助用户构建出更为模块化的代码。

go语言也经常会被用于创建微服务（Microservices）。在微服务架构中，大型应用通常由多个规模较小的独立服务组合而成，这些独立服务通常可以相互替换，并根据他们各自的功能进行组织。比如，日志记录服务会被归类为系统级服务，而开具账单，风险分析这样的服务则会被归类为应用级服务。创建多个规模较小的go服务并将他们组合为单个web应用，这种做法使得我们可以在有需要的时候对应用中的服务进行替换，而整个web应用也会因此变得更加模块化。

http是一种无状态协议，它唯一知道的就是客户端会向服务器发送请求，而服务器则会向客户端返回响应，并且后续发生的请求对之前发生过的请求一无所知。相对的，像FTP,Telnet这类面向连接的协议则会在客户端和服务器之间创建一个持续存在的通信通道（其中Telnet在进行通信时使用的也是请求-响应方式以及客户端-服务器计算模型）。顺带提一下，http1.1也可以通过持久化连接来提升性能。

跟很多互联网协议一样，HTTP也是以纯文本方式而不是二进制方式发送和接受协议数据的。

CGI是一个简单的接口，它允许web服务器与一个独立运行于web服务器进程之外的进程进行对接。

通过CGI与服务器进行对接的程序通常被称为CGI程序，这种程序可以使用任何编程语言编写 ——  这也是我们把这种接口称之为 “ 通用 “ 接口的原因，不过早期的 CGI 程序大多数都是使用 Perl语言编写的。

安全的请求方法 ： 

​	如果一个HTTP方法只要求服务器提供信息而不会对服务器的状态做任何修改，那么这个方法就是安全的（safe)。GET，HEAD，OPTIONS和TRACE都不会对服务器的状态进行修改，所以它们都是安全的方法。与此相反，POST，PUT和DELETE都能够对服务器的状态进行修改（比如说，在处理POST请求时，服务器存储的数据就可能会发生变化），因此这些方法都不是安全的方法。

幂等的请求方法：

​	如果一个HTTP方法在使用相同的数据进行第二次调用的时候，不会对服务器的状态造成任何改变，那么这个方法就是幂等的。根据安全的方法定义，因为所有安全的方法都不会修改服务器状态，所以他们天生就是幂等的。

​	PUT和DELETE虽然不安全，但却是幂等的，这是因为它们在进行第二次调用时都不会改变服务器的状态。

​	相反，因为重复的POST请求时否会改变服务器状态时由服务器自身决定的，所以POST方法既不安全也非幂等。幂等性是一个非常重要的概念。

HTML不支持GET和POST之外的其他HTTP方法。

话虽如此，但流行的浏览器通常都不会只支持HTML一种数据格式 ——  用户可以使用XMLHttpRequest (XHR) 来获得对PUT方法和DELETE方法的支持。

大多数HTTP请求首部都是可选的，宿主（Host）首部字段是HTTP1.1唯一强制要求的首部。

HTTP请求报文：

- 请求行
- 零个或任意多个请求首部
- 一个空行
- 可选的报文主体

HTTP响应报文：

- 状态行
- 零个或任意数量的响应首部
- 一个空行
- 可选的报文主体 

HTTP响应状态码：

- 情报状态码：1XX
- 成功状态码：2XX
- 重定向状态码：3XX
- 客户端错误状态码：4XX
- 服务器错误状态码：5XX

HTTP请求首部：

- Accpet
- Accpet-Charset
- Authorization
- Cookie
- Content-Length
- Content-Type
- Host
- Referrer
- User-Agent

HTTP响应首部：

- Allow
- Content-Length
- Content-Type
- Date
- Location
- Server
- Set-Cookie
- www-Authenticate

URI

​	在URI的各个部分当中，只有 ” 方案名称 “ 和 ”分层部分“ 是必需的。

​	因为每个URL都是一个单独的字符串，所以URL里面是不能够包含空格的。此外，因为问号？和井号#等符号在URL中具有特殊含义，所以这些符号是不能够用于其他用途的。为了避开这些规则，我们需要使用URL编码来对这些特殊符号进行转换（URL编码又称百分号编码）

RFC 3986 定义了URL中的保留字段以及非法保留字符，所有保留字符都需要进行URL编码；URL编码会把保留字符转换成该字符在ASCII编码中对应的字节值（byte value),接着把这个字节值表示为一个两位长的十六进制数字，最后再在这个十六进制数字的前面加上一个百分号（%）。

Web应用被分成了处理器（handler) 和模板引擎（template engine)这两个部分。

处理器 （handler)

​	Web应用中的处理器除了要接受和处理客户端发来的请求，还需要调用模板引擎，然后由模板引擎生成HTML并把数据填充至将要回传给客户端的响应报文当中。

​	用MVC模式来讲，处理器既是控制器（controller) ，也是模型（model)。在理想的MVC模式实现中，控制器应该是 “苗条的”，它应该只包含路由（routing) 代码以及HTTP报文的解包和打包逻辑；而模型则应该是 “丰满的“ ，它应该包含应用的逻辑以及数据。

因为HTTP是一种无连接协议，通过这种协议发送给服务器的请求对服务器之前处理过的请求一无所知，所以应用程序才会以cookie的方式在客户端实现数据持久化，并以session的方式在服务器上实现数据持久化，而不了解这一点的人是很难理解为什么要在不同连接之间使用cookie和session实现信息持久化的。

net/http标准库可以分为客户端和服务器两个部分，库中的结构和函数有些只支持客户端和服务器这两者中的一个，而有些则同时支持客户端和服务器：

- Client，Response，**Header，Request和Cookie**对客户端进行支持

- Server，ServeMux，Handle/HandleFunc，ResponseWriter，**Header，Request和Cookie**则对服务器进行支持

  

SSL证书没有所谓的“品质”和“等级”之分，只有三种不同的类型。                                         SSL证书需要向国际公认的证书证书认证机构（简称CA，Certificate Authority）申请。    CA机构颁发的证书有3种类型：                   
域名型SSL证书（DV SSL）：信任等级普通，只需验证网站的真实性便可颁发证书保护网站；                                                                     企业型SSL证书（OV SSL）：信任等级强，须要验证企业的身份，审核严格，安全性更高；                                                                     增强型SSL证书（EV SSL）：信任等级最高，一般用于银行证券等金融机构，审核严格，安全性最高，同时可以激活绿色网址栏。                     如果是个人博客、中小企业网站和一些传统行业的形象展示类网站，一般来说只需要申请一个域名型SSL证书（DV SSL）就足够了，一方面这类网站确实没有值得加密的信息，而且HTTPS在国内普及率不高，国内网民对这个也不太重视，另一方面DV SSL证书申请流程简洁，费用低。                                                             这块的话国内我用过的是爱名网的SSL证书，性价比高是其次，主要是选择多，能满足我自己需求的前提下还有其他服务，针对我这种小白帮助真的很大，向导式服务，售后不用担心，其他家的暂时没用过，给不了其他意见。

在GO语言中，一个处理器就是一个拥有ServeHTTP方法的接口，这个ServeHTTP方法需要接受两个参数：第一个参数是一个ResponseWriter接口，而第二个参数则是一个指向Request结构的指针。换句话说，任何接口只要拥有一个ServerHTTP方法，并且该方法带有以下签名，那么它就是一个处理器： ServeHTTP(http.ResponseWriter,*http.Request)

处理器与处理器函数：

​	处理器函数实际上就是与处理器拥有相同行为的函数：这些函数与ServeHTTP方法拥有相同的签名，也就是说，它们接受ResponseWriter和指向Request结构的指针作为参数。

​	处理器函数的实现原理是这样的：Go语言拥有一种HandlerFunc函数类型，它可以把一个带有正确签名的函数f转换成一个带有方法f的Handler。换句话说，处理器函数只不过是创建处理器的一种便利方法而已。

```go
// HandleFunc registers the handler function for the given pattern.

func (mux *ServeMux) HandleFunc(pattern string, handler func(ResponseWriter, *Request)) {

​    if handler == nil {

​        panic("http: nil handler")

​    }

​    mux.Handle(pattern, HandlerFunc(handler))

}

// Handle registers the handler for the given pattern

// in the DefaultServeMux.

// The documentation for ServeMux explains how patterns are matched.

func Handle(pattern string, handler Handler) { DefaultServeMux.Handle(pattern, handler) }

// HandleFunc registers the handler function for the given pattern

// in the DefaultServeMux.

// The documentation for ServeMux explains how patterns are matched.

func HandleFunc(pattern string, handler func(ResponseWriter, *Request)) {

​    DefaultServeMux.HandleFunc(pattern, handler)

}
```

​	

虽然处理器函数能够完成跟处理器一样的工作，并且使用处理器函数的代码比使用处理器的代码更为整洁，但是处理器函数并不能完全代替处理器。这是因为在某些情况下，代码可能已经包含了某个接口或者某种类型，这时我们只需要为他们添加ServeHTTP方法就可以将他们转变为处理器了，并且这种转变也有助于构建出更为模块化的Web应用。