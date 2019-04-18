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

3.3.4 串联多个处理器和处理器函数

尽管Go语言并不是一门函数式编程语言，但它也拥有一些函数式编程语言的特性，如函数类型，匿名函数和闭包。

最小惊讶原则：

​	1，避免重复原则：DRY，don't repeat yourself 

​		编程的最基本原则是避免重复。在程序代码中总会有许多结构体，如循环，函数，类等等。一旦你重复某个语		句或概念，就会很容易形成一个抽象体。

​	2，抽象原则：Abstraction Principle

​		与DRY原则相关。要记住，程序代码中每一个重要的功能，只能出现在源代码的一个位置。

​	3，简单原则：Keep It Simple and Stupid

​		简单是软件设计的目标，简单的代码占用时间少，漏洞少，并且易于修改。

​	4，避免创建你不要的代码 Avoid Creating a YAGNI ( You aren't going to need it )

​		除非你需要它，否则别创建新功能

​	5，尽可能做可运行的最简单的事 （Do the simplest thing that could possible work)

​		尽可能做可运行的最简单的事。在编程中，一定要保持简单原则。作为一名程序员不断的反思 ” 如何在工作中做		到简化呢？“ 这将有助于在设计中保持简单的路径。

​	6，别让我思考（ Don‘t make me think )

​		这是Steve Krug 一本书的标题，同时也和编程有关。所编写的代码一定要易于读易于理解，这样别人才会欣		赏，也能够给你提出合理化的建议。相反，若是繁杂难解的程序，其他人总是会避而远之的。

​	7，开闭原则（ Open / Closed Principle）

​		你所编写的软件实体（类，模块，函数等）最好是开源的。这样别人可以拓展开发。不过，对于你的代码，得		限定别人不得修改。换句话说，别人可以基于你的代码进行拓展编写，但却不能修改你的代码。

​	8，代码维护（ Write Code for the Maintainer）

​		一个优秀的代码，应当使本人或是他人在将来都能够对它继续编写或维护。代码维护时，或许本人会比较容易		但对他人却比较麻烦。因此你写的代码要尽可能保证他人能够容易维护。用书中原话说 ” 如果一个维护者不再继		续维护你的代码，很可能他就有想杀了你的冲动。“

​	9，最小惊讶原则（ Principle Of least astonishment )

​		最小惊讶原则通常是在用户界面方面，但同样适用于编写的代码。代码应该尽可能减少让读者惊喜。也就是		说，你编写的代码只需按照项目的要求来填写。其他华丽的功能就不必了，以免弄巧成拙。

​		也称最小意外原则，是设计包括软件在内的一切事务的一条通用规则，它指的是我们在进行设计的时候，应该		做那些合乎常理的事情，使事务的行为总是显而易见，始终如一并且合乎情理。举个例子：如果我们在一扇门		的旁边放置一个按钮，那么人们就会认为这个按钮与这扇门有关，比如，按下按钮门铃会响或者门会自动打开

​		等等。但是如果这个按钮被按下去的时候会关掉走廊的灯光，它就违反了最小惊讶原则，因为这一行为不符合		人们对这个按钮的有预期。

​	10，单一责任原则 （ Single Responsibility Principle )

​		某个代码的功能，应该保证只有单一的明确的执行任务。

​	11，低耦合原则 （ Minimize Coupling ）

​		代码的任何一个部分应该减少对其他区域代码的依赖关系。尽量不要使用共享参数。低耦合往往是完美结构系		统和优秀设计的标志。

​	12，最大限度凝聚原则 （ Maxmize Cohesion )

​		相似的功能代码应该尽量放在一个部分。

​	13，隐藏实现细节 （ Hide Implementation Details )

​		隐藏实现细节原则，当其他功能部分发生变化时，能够尽可能降低对其他组件的影响。

​	14，迪米特法则 （ 又叫做最少知识原则 ）（ Law of Demeter )

​		该代码只和与其有直接关系的部分连接（ 比如：该部分继承的类，包含的对象，参数传递的对象等 ）。



3.3.6 使用其他多路复用器

​	创建一个处理器（Handler）和多路复用器（ServeMux）唯一需要做的就是实现ServeHTTP方法



需要注意的一点是：如果请求报文是由浏览器发送的，那么程序将无法通过URL结构的Fragment字段获取URL的片段部分。本书在第一章就提到过，浏览器在向服务器发送请求之前，会将URL中的片段部分删除掉 ---- 因为服务器接收到的都是不包含片段部分的URL，所以程序自然也无法通过Fragment字段去获取URL的片段部分了，造成这个问题的原因在于浏览器，与我们正在使用的net/http库无关。

URL结构的Fragment字段之所以会存在，是因为并非所有请求都来自浏览器：除了浏览器发送的请求之外，服务器还可能会接收到HTTP客户端库，Angular这样的客户端框架或者某些其他工具发送的请求；此外别忘了，不仅服务器可以使用Request结构，客户端库也同样可以把Request结构用作自己的一部分。

4.2 Go与HTML表单：

​	在绝大多数情况下，POST请求都是通过HTML表单发送的。

PostForm字段只会包含键的表单值，而不包含任何同名键的URL值。

Form字段包含键的表单值和URL值。

MultipartForm字段只包含表单键值对而不包含URL键值对。MultipartForm字段的值不再是一个映射，而是一个包含了两个映射的结构，其中第一个映射的键为字符串，值为字符串组成的切片，而第二个映射则是空的 ---- 这个映射之所以会为空，是因为它是用来记录用户上传的文件的。

FormValue方法和PostFormValue方法都会在需要时自动去调用ParseMultipartForm方法，因此用户并不需要手动去调用ParseMultipartForm方法。

4.2.4 文件

​	multipart / form-data 编码通常用于实现文件上传功能，这种功能需要用到file类型的input标签。

4.4.1 Go与cookie

​	大多数cookie都可以被划分为会话cookie和持久cookie两种类型，而其他类型的cookie通常都是持久的。

​	没有设置Expires字段的cookie通常称为会话cookie或者临时cookie，这种cookie在浏览器关闭的时候就会自动被删除。相对而言，设置了Expires字段你的cookie通常称为持久cookie，这种cookie会一直存中，知道指定的过期时间来临或者被手动删除为止。

4.4.2 将cookie发送至浏览器

​	cookie结构的String方法可以返回一个经过序列化处理的cookie，其中Set-Cookie响应首部的值就是由这些序列化之后的cookie组成的。

5.2 Go的模板引擎

​	用户可以拥有任意多个模板文件，并且这些模板文件可以使用任意后缀名，但它们的类型必须是可读的文本格式。

​	我们可以这样认为：在向ParseFiles传入单个文件时，ParseFiles返回的是一个模板；而在向ParseFIles传入多个文	件时，ParseFiles返回的则是一个模板集合。

​	对模板文件进行语法分析的另一种方法是使用ParseGlob函数，跟ParseFiles只会对给定文件进行语法分析的做法不	同，ParseGlob会对匹配给定模式的所有文件进行语法分析。

​	在绝大多数情况下，程序都是对模板文件进行语法分析，但是在需要时，程序也可以直接对字符串形式的模板进行语	法分析。实际上，所有对模板进行语法分析的收段最终都需要调用Parse方法来执行实际的语法分析操作。

在GO里面，panic会导致正常的执行流程被终止；如果panic是在函数内部产生的，那么函数会将这个panic返回给它的调用者。panic会一直向调用栈的上方传递，直到main函数为止，并且程序也会因此而崩溃。