jQuery 入口函数：
$(document).ready(function()){

}
$(function(){
    alert("hello workd");
})

上面这两种写法一样。


原生js和jQuery入口函数的加载模式不同
通过原生js入口函数可以拿到DOM元素的宽高
通过jQuery入口函数不可以拿到DOM元素的宽高
原生js会等到DOM元素加载完毕并且图片也加载完毕才会执行
jQuery会等到DOM元素加载完毕，但不会等到图片也加载完毕就会执行

原生的js如果编写了多个入口函数，后面编写的会覆盖前面的，而jQuery不会

1.释放$的使用权
    jQuery.noConflict();
    注意点：释放操作必须在编写其他jQuery代码之前，释放之后就不能再使用$了，改为使用jQuery.

2.自定义快捷访问符号
    var jq = jQuery.noConflict();

jQuery的核心函数

    $();就代表调用jQuery的核心函数
    
        1.接受一个函数
            $(function(){
                alert();
            })  //返回一个jQuery对象，对象中保存了找到的DOM元素
    
        2.接受一个字符串
            2.1 接收一个字符串选择器
                var $box1 = $(".box1"); //返回一个jQuery对象，对象中保存了找到的DOM元素
    
            2.2接收一个代码片段
                var $p = $("<p>我是段落</p>"); jQuery会根据传进去的代码片段参数生成一个html元素，
                返回一个jQuery对象，对象中保存了找到的DOM元素
    
        3.接受一个DOM元素
            接收到的DOM元素会被jQuery包装成一个jQuery对象返回给我们。


​        
​    [ jQuery对象其实是一个伪数组。]
​    
​        什么是伪数组: 有0-length-1的属性，并且有length属性


静态方法和实例方法:


js的原生forEach方法，只能遍历真数组，不能遍历伪数组

    利用jQuery的each静态方法遍历数组：
        第一个参数: 当前遍历到的索引
        第二个参数: 遍历到的元素
    注意点: jQuery的each方法是可以遍历伪数组的。


原生js中的map,each和jQuery中的map,each有什么区别?

利用原生JS的map方法遍历
第一个参数: 当前遍历到的元素
第二个参数: 当前遍历到的索引
第三个参数: 当前遍历到的数组

arr.map(function(value, index, array){
    console.log(value, index, array);
})

原生js中的map和原生js中的foreach一样，不能遍历伪数组。

$.map(arr, function(value, index){
    console.log(index, value);
})

第一个参数: 要遍历的数组
第二个参数: 每遍历一个元素之后执行的回调函数
    回调函数的参数：

        第一个参数: 遍历到的元素
        第二个参数: 遍历到的索引

var res=$.map(obj, function(value, index){
    console.log(index, value);
})

var res=$.each(obj, function(value, index){
    console.log(index, value);
})

/* jQuery中的each静态方法和map静态方法的区别:
    each静态方法默认的返回值就是要遍历的元素，也就是第一个参数
    而map静态方法默认的返回值是一个空数组。
    each静态方法不支持在回调函数中对遍历的数组进行处理，而map静态方法可以在回调函数中通过return对遍历的数组进行处理，然后生成一个
    新的数组返回。
*/

jQuery中的其他静态方法:

    1.$.trim()
        作用: 去除字符串两端的空格
        参数: 需要去除空格的字符串
        返回值: 去除空格之后的字符串
    
    2.$.isWindow();
        作用: 判断传入的对象是不是window对象。
        返回值 true/false
    
    3.$.isArray();
        作用: 判断传入的对象是不是array。
        返回值 true/false


    2.$.isFunction();
        作用: 判断传入的对象是不是function。
        返回值 true/false
    
        注意点：jQuery框架本质上是一个函数, 也就是说$.isFunction(jQuery) = true;


​    
页面所有的dom元素加载完毕，jQuery入口函数就会执行。

    $.holdReady(true); 暂停jQuery ready函数的执行
    $.document.ready(function(){
        $.holdReady(false); //恢复jQuery ready的执行
        alert("ready");
    })


<el>:empty : 指的是既没有文本又没有子元素的元素

    :contains 找到包含指定文本内容的元素
    :has  找到包含指定子元素的元素

属性和属性节点
    1.什么是属性
        对象身上保存的变量就是属性
        var p = new Person();
        p.name = "glen"
    2.如何操作属性
        对象.属性名称 = 值      赋值
        对象.属性名称;          取值
        对象["属性名称"] = 值   赋值
        对象["属性名称"]        取值
    3.什么是属性节点
        <span name="glen"></span> : 在标签中添加属性就是属性节点
        在浏览器中找到span这个DOM元素之后，展开看到的都是属性，在attributes属性中保持的所有的内容都是属性节点
        任何对象都有属性，但是只有DOM元素才有属性节点
        属性节点都保存在DOM元素的attributes属性当中
    4.如何操作属性节点
        DOM元素.setAttribute("属性名称", "值");
        DOM元素.getAttributes("属性名称");
    5.属性和属性节点有什么区别
        任何对象都有属性，但是只有DOM元素才有属性节点
        属性节点都保存在DOM元素的attributes属性当中


    1.attr(name|pro|key,val|fn)
    作用: 获取或者设置属性节点的值
    可以传递一个参数， 也可以传递两个参数
    如果传递一个参数， 代表获取属性节点的值
    如果传递两个参数， 代表设置属性节点的值
        注意点: 
            如果是获取：无论找到多少个元素， 都只会返回第一个 元素指定的属性节点的值
            如果是设置: 找到多少个元素，就会设置多少个
            如果是设置：如果设置的属性节点不存在，那么系统会自动新增
    
    2. removeAttr(name1 name2)
        删除属性节点
    
        注意点:
            会删除所有找到的元素的指定属性节点 
    
    3. prop方法不仅能够操作属性，他还能操作属性节点
    
        prop和attr既然都能够操作属性节点，那么两者有什么区别呢：
            console.log($("input").prop("checked")); // 打印出来的结果是true / false
            console.log($("input").attr("checked")); // 打印出来的结果是checked / undefined
    
            jQuery官方推荐在操作属性节点时，具有true和false两个属性的属性节点，如checked, selected, disabled 时使用prop()
            其他的使用attr()


    jQuery样式设置的三种方式：
    
        1.逐个设置
            $("div").css("width", "100px");
            $("div").css("width", "100px");
            $("div").css("width", "100px");
    
        2.链式设置
            $.("div").css("width", "100px").css("width", "100px").css("width", "100px").css("width", "100px")
                jQuery链式操作如果大于3步，建议分开
    
        3.批量设置 (推荐使用这种方式)
            $("div").css({
                width:"100px",
                width:"100px",
                width:"100px"
            })
    
        4.获取css样式值
            console.log($("div").css("background"));
    
        5. scrolltop: 用了获取元素滚动的距离顶部的偏移距离
    
            html或者body标签都可以代表整个网页
    
    jQuery两种事件绑定方式:
        1.eventName(fn);
            编码效率略高 部分事件jQuery没有实现，所以不能添加
            可以添加多个相同或者不同的事件，事件之间不会覆盖
        2.on(eventName, fn);
            编码效率低 所有事件都可以添加
            可以添加多个相同或者不同的事件，事件之间不会覆盖
    
    jQuery事件解绑方式:
        off方法如果不传递参数，会移除所有的事件绑定
        off方法如果传递一个参数， 会移除所有指定类型的事件
        off方法如果传递参数，会移除所有指定类型的指定事件


    jQuery事件冒泡
        1.什么是事件冒泡
        2.如何阻止事件冒泡
        3.什么是默认行为
        4.如何阻止默认行为
onload事件会等到DOM元素加载完毕,并且还会等到资源也加载完毕才会执行

DOMContentLoaded事件只会等到DOM元素加载完毕就会执行回调

在jQuery中each方法中的this指向的是key:value中的value

element.cloneNode(true)和element.cloneNode(false)区别 : 前者会克隆元素内部内容,而后者不会



# jQuery.ajax()



概述 jQuery.ajax(url [,settings])

返回值: XMLHttpRequest

说明:执行一个异步的 HTTP (Ajax)的请求.

jQuery.ajax(url [,settings])

​	url 类型: String 一个用来包含发送请求的URL字符串.

​	settings : 类型 : PlainObject 一个以"{键:值}"组成的AJAX请求设置.所有选项都是可选的. 可以使用$.ajaxSetup()设置任何默认参数.看jQuery.ajax( settings ) 下所有设置的完整列表.

jQuery.ajax( [settings] )

## 	settings

​	类型:PlainObject 一个以"{键:值}" 组成的AJAX设置. 所有选项都是可选的. 可以使用$.ajaxSetup()设置任何默认参数.

​		accepts (默认: 取决于数据类型)

​		类型: PlainObject 一个键/值对集合映射给定的dataType到其的MIME类型, 它可以从发送Accept请求头信息中获得.请求头信息通知服务器该请求需要接受何种类型的返回结果.例如,下面定义一个自定义类型的mycustomtype与请求一起发送:

```java
$.ajax({
2.  accepts: {
3.    mycustomtype: 'application/x-some-custom-type'
4.  },
5. 
6.  // Instructions for how to deserialize a `mycustomtype`
7.  converters: {
8.    'text mycustomtype': function(result) {
9.      // Do Stuff
10.      return newresult;
11.    }
12.  },
13. 
14.  // Expect a `mycustomtype` back from server
15.  dataType: 'mycustomtype'
16.});

```

注意:对于这种类型,为了使其正常工作,您将需要在converters中指定补充项.

## async( 默认:true )

类型:Boolean

默认设置下,所有请求均为异步请求(也就是说默认设置为true. 如果需要发送同步请求,请将此选项设置为false. 跨域请求和dataType:"jsonp" 请求不支持同步操作. 注意,同步请求将锁住浏览器,用户其他操作必须等待请求完成才可以执行.从jQuery1.8开始,jqXHR($.Deferred)中使用async:false 已经过时. 您必须使用的success/error/complete的回调选项代替相应的jqXHR对象的方法,比如jqXHR.done()

## beforeSend

类型: Function(jqXHR jxXHR, PlainObject settings)

请求发送前的回调函数,用来修改请求发送前jqXHR ( 在jQuery1.4.x中,XMLHttpRequest ) 对象,此功能用来设置自定义HTTP头信息,等到. 该jqXHR和设置对象作为参数传递.这是一个Ajax事件. 在beforeSend函数中返回false将取消这个请求.**从jQuery1.5开始**,beforeSend选项将被访问,不管请求的类型

## cache( 默认: true,dataType为"script"和"jsonp" 时默认为false )

类型:Boolean

如果设置为false, 浏览器将不缓存此页面.注意:设置cache为false 将在HEAD和GET请求中正常工作. 它的工作原理是在GET 请求参数中附加"_={timestamp}" . 该参数不是其他请求所必须的,除了在IE8中,当一个POST请求一个已经用GET请求过的URL.

## complete

类型:Function(jqXHR jqXHR, String textStatus)

请求完成后回调函数(请求 success 和 error之后均调用). 这个回调函数得到2个参数:jqXHR(在jQuery1.4.x 中是XMLHTTPRequest)对象和一个描述请求状态的字符串("success","notmodified","nocontent","error","timeout","abort",或者"parseerror").

## contents

类型:PlainObject 

一个以"{字符串/正则表达式}"配对的对象,根据给定的内容类型,解析请求的返回结果.

## contentType

default: 'application/x-www-form-urlencoded; charset=utf-8'

Type:Boolean or String

当将数据发送到服务器时,使用该内容类型.默认值适合大多数情况. 如果你明确地传递了一个内容类型(Content-Type)给$.ajax(),那么他总是会发送给服务器(即使没有数据要发送). 从jQuery1.6开始,你可以传递false来告诉jQuery,没有设置任何内容类型头信息.注意:W3C的XMLHttpRequest的规范规定,数据将总是使用UTF-8字符集传递给服务器;指定其他字符集无法强制浏览器更改编码.注意:对于跨域请求,内容类型设置为application/x-www-form-urlencoded, multipart/form-data,或text/plain以外,将触发浏览器发送一个预检OPTIONS请求到服务器.

## context

类型: Object

这个对象用于设置Ajax相关回调函数的上下文.默认情况下,这个上下文是一个ajax请求使用的参数设置对象,($.ajaxSettings 合并独傲这个设置,传递给$.ajax). 比如指定一个DOM元素作为context参数,这样就设置了complete回调函数的上下文为这个DOM元素.就像这样:

```javascript
$.ajax({
2.  url: "test.html",
3.  context: document.body
4.}).done(function() {
5.  $(this).addClass("done");
6.});

```



## converters ( 默认:{ "* text":windows.String, "text html":true, "text json":jQuery.parseJSON,"text xml":jQuery.parseXML } )

类型:PlainObject

一个数据类型到数据类型转换器的对象.每个转换器的值是一个函数,返回经转换后的请求结果.



## crossDomain ( 默认: 同域请求为false, 跨域请求为true)

类型: Boolean 如果你想在同一域中强制跨域请求(如JSONP形式),例如,想服务器端重定向到另一个域,那么需要将crossDomain设置为true.



## data

类型:PlainObject或String 或Array

发送到服务器的数据.它被转换成一个查询字符串,如果已经是一个字符串的话就不会转换.查询字符串将被追加到GET请求的URL后面.参加processData选项说明,以防止这种自动转换.对象必须为"{键:值}"格式. 如果这个参数是一个数组,jQuery会按照traditional参数的值,将自动转换为一个同名的多值查询字符串(查看下面的说明).如: {foo:["bar1","bar2"]}转换为'&foo=bar1&foo=bar2'

## dataFilter

类型:Function( String data, String type) => Anything

一个函数被用来处理XMLHttpRequest的原始相应数据.这是一个预过滤功能,净化响应. 您应该返回安全数据.提供data和type两个参数:data 是Ajax返回的原始数据,type是调用jQuery.ajax时提供的dataType参数.

## dataType(default: Intelligent Guess (xml,json, script, or html ))

Type: String

从服务器返回你期望的数据类型.如果没有指定,jQuery将尝试通过MIME类型的响应信息来智能判断(一个XML MIME类型就被识别为XML,在1.4中 JSON将生成一个JavaScript对象,在1.4中script将执行改脚本,其他任何类型会返回一个字符串). 可用的类型(以及结果作为第一个参数传递给成功回调函数)有:

​	"xml" : 返回XML文档,可以通过jQuery处理.]

​	"html" : 返回纯文本HTML文本; 包含的script标签会在插入DOM时执行.

​	"script" : 把响应的结果当作JavaScript执行, 并将其当作纯文本返回. 默认情况下会通过在URL 中附加查询字符串变量,

_=[TIMESCRIPT] ,禁用缓存结果,除非设置了cache参数为true. 注意:在远程请求时(不在同一个域下),所有的POST请求都将转为GET请求.(因为将使用DOM的script标签来加载)

"json" : 把响应的结果当作JSON执行,并返回一个JavaScript对象.跨域"json"请求转换为"jsonp",除非改请求在其请求选项中设置了jsonp:false . JSON数据以严格的方式解析; 任何畸形的JSON将被拒绝,并且抛出解析错误信息.在jQuery1.9中,一个空响应也将被拒绝;服务器应该返回null或{}响应代替. (见json.org的更多信息,正确的JSON格式) 

"jsonp" : 以JSONP的方式载入JSON数据块.会自动在所请求得URL最后添加"?callback=?" .默认情况下会通过在URL中附加查询字符串变量, _=[TIMESTAMP], 禁用缓存结果,除非设置了cache参数为true.

"text": 返回纯文本字符串.

多个用空格分隔得值:从jQuery1.5开始,jQuery可以内容类型(Content-Type)头收到并转换一个您需要得数据类型.例如,如果你想要一个文本响应为XML处理,使用"text xml" 数据类型. 您也可以将一个JSONP的请求,以文本形式接受,并用jQuery以XML解析:"jsonp text xml" . 同样地可以使用"jsonp xml" 简写,首先会尝试从jsonp到xml的转换,如果转换失败,就先将jsonp转换成text,然后再由text转换成xml.

## error

类型:Function(jqXHR jxXHR, String textStatus, String errorThrown)

请求失败时调用此函数.有以下三个参数:jqXHR(在jQuery1.4.x 前为XMLHttpRequest)对象,描述发生错误类型的一个字符串和捕获的异常对象. 如果发生了错误,错误信息(第二个参数)除了得到null之外,还可能是"timeout", "error", "abort",和"parsererror". 当一个HTTP错误发生时,errorThrown接受HTTP状态的文本部分,比如:"Not Found"(没有找到)或者"Internal Server Error"( 服务器内部错误 ). 从jQuery 1.5开始,在error设置可以接受函数组成的数组.每个函数将有依次被调用. 这是一个Ajax Event.

## global(默认为: true)

类型:Boolean

无论怎么样这个请求将触发全局AJAX事件处理程序. 默认是true.设置为false 将不会触发全局AJAX事件,如ajaxStart 或者ajaxStop. 这可以用来控制各种Ajax Event.

## headers(默认为: { } )

类型:PlainObject 

一个额外的"键:值}" 对映射到请求发一起送.此设置会在beforeSend函数调用之前被设置;因此,请求头中的设置值,会被beforeSend函数内的设置覆盖.

## ifModified( 默认: false )

类型:Boolean 

只有上次请求响应改变时,才允许请求成功.使用HTTP包Last-Modified头信息判断.默认值是false.忽略HTTP头信息.在jQuery1.4中,他也会检查错误服务器指定的'etag'来确定数据没有被修改过.

## isLocal(默认: 取决于当前的位置协议)

类型:Boolean 允许当前环境被认定为"本地" (如文件系统) , 即使jQuery默认情况下不会这么做.以下协议目前公认为本地:

file, *-extension, and widget. 如果isLocal设置需要修改,建议在$.ajaxSetup()方法中这样做一次

## jsonp

类型:String或者Boolean

在一个JSONP请求中重写回调函数的名字. 这个值用来替代在"callback=?"这种GET或POST请求中URL参数里的"callback"部分,比如{jsonp:'onJsonPLoad'} 会导致将"onJsonPLoad=?" 传给服务器.在jQuery1.5中,设置jsonp选项为false,阻止了jQuery从加入"?callback"字符串的URL或试图使用"=?"转换.在这种情况下,你也应该明确设置jsonpCallback设置.例如,{jsonp:false, jsonpCallback:"callbackName"}. 如果你不信任你的Ajax请求的目标,出于安全原因,考虑设置jsonp属性为false.

## jsonpCallback 

类型:String, Function

为jsonp请求指定一个回调函数名.这个值将用来取代jQuery自动生成的随机函数名.这注意用来让jQuery生成一个独特的函数名,这样管理请求更容易,也能方便地提供回调函数和错误处理.你也可以在想让浏览器缓存GET请求的时候,指定这个回调函数名.从jQuery1.5开始,你也可以使用一个函数作为改参数设置,在这种情况下,该函数的返回值就是jsonpCallback的结果.

## method(defalut:'GET')

Type:String

HTTP请求方法(比如:"POST","GET","PUT") .. 1.9之前使用type选项

## mimeType

类型:String 一个mime类型用来覆盖XHR的MIME类型

## password

类型:String 用于响应HTTP访问认证的密码

## processData(默认: true)

类型:Boolean

默认情况下,通过data选项传递进来的数据,如果是一个对象(技术上讲只要不是字符串),都会处理转换成一个查询字符串,以配合默认内容类型 "application/x-www-form-urlencoded". 如果要发送DOM树信息或其他不希望转换的信息,请设置为false.

## scriptCharset

类型:String

仅适用于当"script"传输使用时(例如,跨域的"jsonp"或dataType选项为"script" 和 "GET"类型.请求中使用在script标签上设置charset属性.通常只在本地和远程的内容编码不同时使用.

## statusCode(默认:{ })

类型:PlainObject 

一个HTTP响应状态码和当请求响应相应的状态码时执行的函数组成的对象.例如: 下面的代码将在http响应状态码为404是弹出"page not found".

```javascript
$.ajax({
2.  statusCode: {
3.    404: function() {
4.      alert("page not found");
5.    }
6.  }
7.});
```

如果请求成功,响应状态码对应的函数会带着success 回调函数相同的参数; 如果请求结果是错误的(包含3xx之类的重定向),他们会采用error回调函数相同的参数

## success 

Type:Function(Anything data, String textStatus, jqXHR jaXHR)

请求成功后的回调函数.这个函数传递3个参数:从服务器返回的数据,并根据dataType参数进行处理后的数据或dataFilter回调函数,如果指定的话;一个描述状态的字符串;还有jqXHR(在jQuery1.4.x前为XMLHttpRequest)对象.在jQuery1.5, 成功设置可以接受一个函数数组,每个函数将被依次调用.这是一个Ajax Event

## timeout

类型:Number

设置请求超时时间(毫秒).此设置将覆盖$.ajaxSetup()里的全局设置.超时周期开始于$.ajax访问成功的那个时间点;如果几个其他请求都在进步并且浏览器又没有可用的链接,它有可能在被发送前就超时了.在jQuery1.4.x和前面的版本中,如果请求超时,XMLHttpRequest 对象是处于无效状态;访问任何对象的成员可能会抛出一个异常.只有在Firefox 3.0+, script和JSONP请求在超时后不能被取消;该脚本将运行即使超时后到达.

## traditional

类型:Boolean

如果你想要用传统的方法来序列化数据,那么就设置为true.请参考工具分类下面的jQuery.param方法.

## type(默认:'GET' )

类型:String

method选项的别名.如果你使用jQuery1.9.0之前的版本,你需要使用type选项

## url(默认:当前页面地址)

类型:String

发送请求的地址

## username

类型:String  用于响应HTTP访问认证请求的用户名

## xhr(默认: 当可用的ActiveXObject(IE)中,否则为XMLHttpRequest)

类型:Function() 回调创建XMLHttpRequest对象.当可用是默认为ActiveXObect(IE)中,否则为XMLHttpRequest. 提供覆盖你自己的执行XMLHttpRequest或增强工厂

## xhrFields

类型:PlainObect 一对文件名-文件值" 组成的映射,用于设定原生的XHR对象.例如,如果需要的话,在进行跨域请求时,你可以用它来设置withCredentials为true.

```javascript
$.ajax({
2.   url: a_cross_domain_url,
3.   xhrFields: {
4.      withCredentials: true
5.   }
6.});
```

在jQuery1.5中, withCredentials属性不会传递给原生的XHR 从而对于需要使用此属性的CORS请求,则只能忽略这个属性. 出于这个原因,我们建议您使用jQuery1.5.1+ ,如果您需要使用它.

jQuery 发送的所有ajax请求,内部都会通过调用$.ajax()函数来实现. 通常没有必要直接调用这个函数,可以使用几个已经封装的简单方法,如$.get()和.load() . 如果你需要用到那些不常见的选项,那么, $.ajax()使用起来更灵活.

在简单地说,$.ajax()函数可以不带参数调用:

```javascript
$.ajax();
```

注意: 所有的选项都可以通过$.ajaxSetup()函数来全局设置

这个示例中,不使用选项,加载当前页面的内容,但其结果没用的.若要使用结果,我们可以实现的回调功能之一.

jqXHR对象

从jQuery1.5开始, $.ajax()返回XMLHttpRequest(jqXHR对象),该对象是浏览器的原生的XMLHttpRequest对象的一个超集.例如,它包含responseText和responseXML属性,以及一个getResponseHeader()方法.当传输机制不是XMLHttpRequest时(例如,一个JSONP请求脚本,返回一个脚本tag时),jqXHR对象尽可能的模拟原生的XHR功能.

从jQuery1.5.1 开始, jqXHR对象还包含了overrideMimeType方法(它在jQuery 1.4.x中是有效的,但是在jQuery 1.5中暂时的被移除). .overrideMimeType()方法可能用在beforeSend()的回调函数中,例如,修改响应的Content-Type信息头:

```
$.ajax({
2.  url: "http://fiddle.jshell.net/favicon.png",
3.  beforeSend: function ( xhr ) {
4.    xhr.overrideMimeType("text/plain; charset=x-user-defined");
5.  }
6.}).done(function ( data ) {
7.  if( console && console.log ) {
8.    console.log("Sample of data:", data.slice(0, 100));
9.  }
10.});
```

从jQuery 1.5开始, $.ajax()返回的jqXHR对象实现了Promise接口, 使它拥有了Promise的所有属性,方法,行为.为了让回调函数的名字统一,便于在$.ajax()中使用.jqXHR也提供 .error() .success() 和.complete()方法. 这些方法都带有一个参数, 该参数使一个函数, 此函数在$.ajax()请求结束时被调用,并且这个函数接受的参数,与调用$.ajax()函数时的参数一致,这将允许你在一次请求时,对多个回到函数进行赋值,甚至允许你在请求已经完成后,对回调函数进行赋值(如果请求已经完成,则回调函数会被立刻调用).

jqXHR.done(function (data, textStatus ,jqXHR {}));

一个可供选择的success回调选项的构造函数,请参阅deferred.done()的实现细节.

jqXHR.fail(function(jqXHR,textStatus,errorThrown){});

一种可供选择的error回调选项的构造函数, .fail()方法取代了过时的 .error()方法. 请参阅deferred.fail()的实现细节.

jqXHR.always(function(data|jqXHR,textStatus,errorThrown));

一种可供选择的complete回调选项的构造函数, .always()方法取代了的过时的.complete()方法.

在响应一个成功的请求后,该函数的参数和.done()的参数是相同的: data,textStatus,和jqXHR对象,对于失败的情况,参数和.fail()的参数是相同的:jqXHR对象,textStatus,和errorThrown. 请参阅deferred.always()的实现细节.

.jqXHR.then(function(data,textStatus,jqXHR){},function(jqXHR,textStatus,errorThrown){});

包含了.done()和.fail()方法的功能,(从jQuery1,8开始)允许底层被操纵.请参阅deferred.then()的实现细节.

推荐使用的注意事项:jqXHR.success(),jqXHR.error(),和jqXHR.complete()回调从jQuery3.0删除,你可以使用jqXHR.done(),jqXHR.fail(),和jqXHR.always()代替.

```javascript
// Assign handlers immediately after making the request,
2.// and remember the jqxhr object for this request
3.var jqxhr = $.ajax( "example.php" )
4.    .done(function() { alert("success"); })
5.    .fail(function() { alert("error"); })
6.    .always(function() { alert("complete"); });
7. 
8.// perform other work here ...
9. 
10.// Set another completion function for the request above
11.jqxhr.always(function() { alert("second complete"); });
```

this 在所有的回调中引用,是这个对象在传递给$.ajax的设置中上下文;如果没有指定context(上下文),this 引用的是Ajax设置的本身.

为了向后兼容XMLHttpRequest, - jqXHR对象将公开下列属性和方法:

- readyState
- status
- statusText
- responseXML and/or responseText 当底层的请求分别作出XML和/ 或文本响应
- setRequestHeader(name,value)从标准出发,通过替换旧的值为新的值, 而不是替换新值到旧值
- getAllResponseHeaders()
- getResponseHeader()
- abort()

假如没有onreadystatechange属性,因为不同的状态可以分别在success,error, complete,和statusCode方法中进行处理

## Data Types ( 数据类型 )

$.ajax()调用不同类型的响应,被传递到成功处理函数之前,会经过不同种类的预处理.预处理的类型取决于由更加接近默认的Content-Type响应,但可以明确使用dataType选项进行设置.如果提供了dataType选项,响应的Content-Type头信息将被忽略

有效的数据类型是text,html,xml,json,jsonp,和script

如果指定的是text或html, 则不会预处理.这些数据被简单地传给成功处理函数,并通过该jqXHR对象的responseText属性获得的.

如果指定的是xml,响应结果作为XMLDocument, 在传递给成功处理函数之前使用jQuery.parseXML进行解析,XML文档是可以通过jqXHR对象的responseXML属性获得的.

如果指定的是json, 响应结果作为一个对象,在传递给成功处理函数之前使用jQuery.parseJSON进行解析.解析后的JSON对象可以通过该jqXHR对象的responseJSON属性获得的.

如果指定的是script,$.ajax()执行这段JavaScript ,这段JavaScript从服务器接收到,在传递给成功处理函数之前是一个字符串.

如果指定的是jsonp,$.ajax()会自动在请求的URL后面增加一个查询字符串参数callback=? (默认) . 传递给$.ajax()设置中的jsonp和jsonpCallback 属性可以被用来指定,分别为查询字符串参数的名称和JSONP回调函数的名称.服务器返回有效的JavaScript, 传递JSON响应到回调函数( 例如,fightHandler({"code":"CA1998","price":1780,"tickets":5});等).在包含JSON对象的相应结果传递给成功处理函数之前,$.ajax()将执行返回的JavaScript,调用JSONP回调函数.

## Sending Data to the Server ( 发送数据到服务器 )

默认情况下,Ajax请求使用GET方法. 如果要使用POST方法,可以设定type参数值. 这个选项也会影响data 选项中的内容如何发送到服务器, POST数据将被发送到服务器使用UTF-8字符集,根据W3C XMLHttpRequest 的标准.

data 选项既可以包含一个查询字符串,比如key1=value&key2=value2 也可以是一个映射,比如{key1:'value1',key2: 'value2'}. 如果使用了后者的形式,则数据再发送前会用jQuery.param()将其转换成查询字符串.这个处理过程也可以通过设置processData选项为false来回避.如果我们希望发送一个XML对象给服务器时,这种处理可能并不合适,并且再这种情况下,我们也应当改变contentType选项的值,用其他合适的MIME类型来取代默认的application/x-www-form-urlencoded.

Advanced Options( 高级选项 )

global 选项用于阻止相应注册的回调函数,比如.ajaxSend(), .ajaxError() , 以及类似的方法. 这在有些时候很有用, 比如发送的请求非常频繁且简短的时候,就可以在.ajaxSend()里禁用这个.跨域脚本和JSONP请求,全局选项设置为false.更多关于这些方法的详细信息,请参阅下面的内容.

如果服务器需要HTTP认证,可以使用用户名和密码可以通过 username 和 password 选项来设置

Ajax请求是限时的,所有错误警告被捕获处理后,可以用来提升用户体验.请求超时这个参数通常就保留其默认值,要不就通过$.ajaxSetup()来全局设定,很少为特定的请求重新设置timeout选项.

默认情况下,请求总会被发出去,但浏览器有可能从他的缓存中调取数据.要禁止使用缓存的结果,可以设置为cache参数为false. 如果希望判断数据自从下次请求后没有更改过就报告出错的话,可以设置ifModified 为true.

scriptCharset 允许给<script> 标签的请求设定一个特定的字符集,用于script或者jsonp类似的数据.当脚本和页面字符集不同时,这特别好用.

Ajax的第一个字母时"asynchronous"的开头字母,这意味着所有的操作都是并行的,完成的顺序没有前后关系.$.ajax()的async参数总是设置成true,这标志着在请求开始后,其他代码依然能够执行.强烈不建议把这个选项设置成false,这意味着所有的请求都不再是异步的了,这也会导致浏览器被锁死,

$.ajax()函数返回他创建的XMLHttpRequest对象,通常,jQuery只在内部处理并创建这个对象,但用户也可以通过xhr选项来传递一个自己创建的xhr对象,返回的对象通常已经被丢弃了,但依然提供一个底层接口来观察和操控请求.比如说,调用对象上的.abort()可以在请求完成前挂起请求.

目前,在Firefox中有一个bug,虽然.getResponseHeader('Content-Type')返回一个非空的字符串,但是.getAllResponseHeaders()还是返回空字符串,在Firefox中使用jQuery不支持自动解码JSON CORS响应

重写jQuery.ajaxSettings.xhr 的一种解决方案,如下:

```javascript
(function () {
2.  var _super = jQuery.ajaxSettings.xhr,
3.    xhrCorsHeaders = [ "Cache-Control", "Content-Language", "Content-Type", "Expires", "Last-Modified", "Pragma" ];
4. 
5.  jQuery.ajaxSettings.xhr = function () {
6.    var xhr = _super(),
7.      getAllResponseHeaders = xhr.getAllResponseHeaders;
8. 
9.    xhr.getAllResponseHeaders = function () {
10.      var allHeaders = "";
11.      try {
12.        allHeaders = getAllResponseHeaders.apply( xhr );
13.        if ( allHeaders ) {
14.          return allHeaders;
15.        }
16.      } catch ( e ) {
17.      }
18. 
19.      $.each( xhrCorsHeaders, function ( i, headerName ) {
20.        if ( xhr.getResponseHeader( headerName ) ) {
21.          allHeaders += headerName + ": " + xhr.getResponseHeader( headerName ) + "\n";
22.        }
23.      });
24.      return allHeaders;
25.    };
26. 
27.    return xhr;
28.  };
29.})();
```

## Extending Ajax

从jQuery1.5开始,jQuery的Ajax 实现包括预prefilters, transport和传输,让您更加灵活的扩展Ajax. 如需有关这些先进功能的信息.

## Using Converters( 使用转换器 )

$.ajax()的转换器支持的数据类型映射到其他数据类型.但是,如果你想要把自定义的数据类型映射到一个已知的类型(json等), 您必须contents选项在响应的Content-Type和实际的数据类型之间添加的一个相关的转换函数:

```javascript
$.ajaxSetup({
2.  contents: {
3.    mycustomtype: /mycustomtype/
4.  },
5.  converters: {
6.    "mycustomtype json": function ( result ) {
7.      // do stuff
8.      return newresult;
9.    }
10.  }
11.});
```

这额外的对象是必要的,因为响应内容类型( Content-Types) 和数据类型从来没有一个严格的一对一对应关系(正则表达式表示结果)

转换一个支持的类型( 例如text,json)成自定义数据类型,然后再返回,使用另一个直通转换器:

```javascript
$.ajaxSetup({
2.  contents: {
3.    mycustomtype: /mycustomtype/
4.  },
5.  converters: {
6.    "text mycustomtype": true,
7.    "mycustomtype json": function ( result ) {
8.      // do stuff
9.      return newresult;
10.    }
11.  }
12.});
```

现在上面的代码允许通过从text为mycustomtype ,进而, mycustomtype 转换为json. 

## Additional Notes: (其他注意事项:)

- 由于浏览器的安全限制,大多数'Ajax'的要求,均采用同一起源的政策;该请求不能成功地检索来自不同的域, 子域或协议的数据
- script和JSONP形式请求不受同源策略的限制



# ajaxComplete()

返回值:jQuery

描述:当Ajax请求完成后注册一个回调函数,这是一个AjaxEvent.

​	.ajaxComplete( handler )

​		handler

​			类型: Function( Event event, jqXHR jqXHR, PlainObject ajaxOptions)

​			被调用的函数.

每当一个Ajax请求完成,jQuery 就会触发ajaxComplete事件,在这个时间点所有处理函数会使用.ajaxComplete()方法注册并执行.

观察活动中的这种方法,建立一个基本的Ajax加载请求:

```html
<div class="trigger">Trigger</div>
<div class="result"></div>
<div class="log"></div>
```

在document上绑定事件处理器:

```javascript
$(document).ajaxComplete(function() {
	$( ".log" ).text( "Triggered ajaxComplete handler." );
});
```

现在,我们可以使用任何的jQuery方法构建一个Ajax请求:

```javascript
$( ".trigger" ).click(function() {
2. $( ".result" ).load( "ajax/test.html" );
3.});
```

当我们点击class为trigger 的元素并且ajax请求完成,这个信息就会显示.

无论哪一个Ajax请求被完成,所有的ajaxComplete处理函数都将被执行.如果我们必须区分不同的请求,我们可以使参数传递给这个处理函数.他是通过事件对象,XMLHttpRequest 对象和设置对象中使用的请求,做每一次ajaxComplete处理器执行的.举个示例,我们能限制我们的回调到只处理事件处理每一特定的URL:

```javascript
$( document ).ajaxComplete(function( event, xhr, settings ) {
2.  if ( settings.url === "ajax/test.html" ) {
3.    $( ".log" ).text( "Triggered ajaxComplete handler. The result is " +
4.      xhr.responseText );
5.  }
6.});
```

注意:您可以通过查看xhr.responseText获取返回的AJAX内容

## 其他注意事项:

- 在jQuery1.9中,jQuery全局AJAX事件的所有处理程序, 包括那些.ajaxComplete()添加的方法,必须附加到document上.
- 如果$.ajax()或$.ajaxSetup()调用时,global 选项设置为false, .ajaxComplete()将不会触发.

## 示例

AJAX请求完成时执行函数.

jQuery代码:

```javascript
$("#msg").ajaxComplete(function(event,request, settings){
2.   $(this).append("<li>请求完成.</li>");
3. });
```

当AJAX请求正在进行时显示"正在加载" 的指示:

jQuery代码:

```javascript
$("#txt").ajaxStart(function(){
2.  $("#wait").css("display","block");
3.});
4.$("#txt").ajaxComplete(function(){
5.  $("#wait").css("display","none");
6.});
```



# load()



概述 .load(url [.data] [.complete(responseText, textStatus, XMLHttpRequest)])

返回值: jQuery

描述: 从服务器载入数据并且将返回的HTML代码插入至匹配的元素中.

> .load( url [,data] [,complete(responseText, textStatus, XMLHttpRequest )])

## url

类型String  一个包含发送请求的URL字符串

## data

类型: PlainObject. String  向服务器发送请求的Key/value参数, 例如{name: "手册网", age:23}

## complete(responseText, textStatus, XMLHttpRequest)

类型:Function()

当请求成功后执行的回调函数.

> ## 注意:事件处理函数中也有一个方法叫.load(). jQuery根据传递给它的参数设置来确定使用哪个方法执行.

这个方法是从服务器获取数据最简单的方法.除了不是全局函数,这个方法和$.get(url,data,success)基本相同,它有一个隐含的回调函数.当他检查到一个成功的请求(i.e. 当textStatus 是" success " 或者 " notmodified ")时,.load()方法将返回的HTML内容数据设置到相匹配的节点中.这就意味着大多数采用这个方法可以很简单.

```javascript
$('#result').load('ajax/test.html');
```

如果选择器没有匹配的元素 --------- 在这种情况下, 如果document 不包含id = "result "的元素 - 这个Ajax请求将不会被发送出去.

如果提供回调,都将在执行后进行后处理

## Callback Function

如果提供了"complete" 回调函数,它将在函数 处理完之后,并且HTML已经被插入完时被调用.回调函数会在每个匹配的元素上被调用一次,并且this 始终指向当前正在处理的DOM元素.

```javascript
$('#result').load('ajax/test.html', function() {
2.  alert('Load was performed.');
3.});
```

在上文的两个示例中,如果当前的文件不包含ID为"result" 的元素,那么.load()方法将不被执行

## Request Method( 请求方法 )

默认使用GET方式,如果data参数提供一个对象,那么使用POST方式

## Loading Page Fragments( 加载页面片段 )

.load()方法, 不像$.get()那样,允许我们使用在url中添加特定参数的特殊语法,来实现可以指定要插入哪一部分远程文档. 如果url参数的字符串中包含一个或多个空格,那么第一个空格后面的内容,会被当成是jQuery的选择器,从而决定应该加载返回结果中的哪部分内容. 注: 第一个空格后面是一个jQuery选择器,返回的内容中匹配该选择器的内容将被载入到页面中.

我们可以修改上述示例中,只有#container的一部分被载入到页面中:

```javascript
$('#result').load('ajax/test.html #container');
```

当这种方法执行,它将检索ajax/test.html 返回的页面内容.jQuery会获取ID为container元素的内容,并且插入到ID为result元素,而其他未被检索到的元素将被废弃

jQuery使用浏览器的.innerHTML属性取解析检索到的文档,并将其插入到当前文档中.在此过程中,浏览器通常会过滤文档中的一些元素,比如<html>,<title>, 或者<head>元素.其结果是,由.load()方法返回的元素与从浏览器中直接获取到的文档内容,可能是并不完全一样的.

## Script Execution (脚本执行)

当使用URL参数中没有后面跟选择器表达式时,那么传递给.html()的返回内容中,是含有脚本的.在它们被丢弃之前,脚本是会被执行的.但如果调用.load()时,即使在url参数中添加了选择器表达式,但在DOM被更新之前,脚本会被删除. 因此脚本不会被执行.下面的示例分别演示了这两种情况:

任何加载到#a中的javascript脚本,将会作为文档的一部分而被执行.

```javascript
$('#a').load('article.html');
```

然而在以下情况下,脚本块将从被加载到#b的document 中被剥离出来,而不执行:

```javascript
$('#b').load('article.html #target');
```



Additional Notes: (其他注意事项: )

- 由于浏览器的安全限制,大多数"Ajax"的要求,均采用同源的政策;该请求不能成功地检索来自不同的域,子域,或协议的数据

## 示例:

加载文章侧边栏导航部分至一个无序列表

HTML代码:

```javascript
<b>jQuery Links:</b>
2.<ul id="links"></ul>
```

jQuery代码:

```javascript
$("#links").load("/Main_Page #p-Getting-Started li");
```



## 示例:

​	加载feeds.html文件的内容.

jQuery 代码:

```javascript
$("#feeds").load("feeds.html");
```

## 实例

​	同上,但是以POST形式发送附加参数并在成功时显示信息

jQuery代码:

```javascript
$("#feeds").load("feeds.php", {limit: 25}, function(){
2.   alert("The last 25 entries in the feed have been loaded");
3. });
```

实例

​	在一个有序列表中,加载主页的页脚导航

```html
<!doctype html>
2.<html lang="en">
3.<head>
4.  <meta charset="utf-8">
5.  <title>load demo</title>
6.  <style>
7.  body {
8.    font-size: 12px;
9.    font-family: Arial;
10.  }
11.  </style>
12.  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
13.</head>
14.<body>
15. 
16.<b>Projects:</b>
17.<ol id="new-projects"></ol>
18. 
19.<script>
20.$( "#new-projects" ).load( "/resources/load.html #projects li" );
21.</script>
22. 
23.</body>
24.</html>
```

## 实例:

显示一个信息如果Ajax请求遭遇一个错误

```javascript
<!DOCTYPE html>
2.<html>
3.<head>
4.  <style>
5.  body{ font-size: 12px; font-family: Arial; }
6.  </style>
7.  <script src="http://code.jquery.com/jquery-latest.js"></script>
8. </head>
9.<body>
10. 
11.<b>Successful Response (should be blank):</b>
12.<div id="success"></div>
13.<b>Error Response:</b>
14.<div id="error"></div>
15. 
16.<script>
17.$("#success").load("/not-here.php", function(response, status, xhr) {
18.  if (status == "error") {
19.    var msg = "Sorry but there was an error: ";
20.    $("#error").html(msg + xhr.status + " " + xhr.statusText);
21.  }
22.});
23.  </script>
24. 
25.</body>
26.</html>
```

## 实例

将feeds.html 文件载入到ID位feeds的DIV.

```javascript
$("#feeds").load("feeds.html");
```

## Result

```html
<div id="feeds"><b>45</b> feeds found.</div>
```

## 实例

​	发送数组形式的data参数到服务器

```javascript
$("#objectID").load("test.php", { 'choices[]': ["Jon", "Susan"] } );
```

## 实例

​	发送数组形式的data参数到服务器.

```javascript
$("#objectID").load("test.php", { 'choices[]': ["Jon", "Susan"] } );
```

实例

​	同上,但会使用POST额外的参数到服务器,并且当服务器响应完成后,回调函数会被执行

```javascript
$("#feeds").load("feeds.php", {limit: 25}, function(){
	alert("The last 25 entries in the feed have been loaded");
});
```



# ajaxSend()

概述 .ajaxSend( handler(event , jqXHR, ajaxOptions ))

返回值: jQuery

## 描述: 在Ajax请求发送之前绑定一个要执行的函数,这是一个Ajax Event.

.ajaxSend( handler(event,jqXHR,ajaxOptions ))

handler(event , jqXHR, ajaxOptions)

每当一个Ajax请求即将发送,jQuery就会触发ajaxSend事件,在这个时间点所有的处理函数都会使用.ajaxSend()方法注册并执行.

观察这种方法,建立一个具体的Ajax加载请求:

```html
<div class="trigger">Trigger</div>
2.<div class="result"></div>
3.<div class="log"></div>
```

在document上绑定事件处理器:

```javascript
$(document).ajaxSend(function() {
2.  $( ".log" ).text( "Triggered ajaxSend handler." );
3.});
```

现在,我们可以使用任何的jQuery方法构建一个Ajax请求:

```javascript
$( ".trigger" ).click(function() {
2.  $( ".result" ).load( "ajax/test.html" );
3.});
```

当我们点击class为 trigger 的元素并且Ajax请求即将开始,这个信息就会显示

## 注,下面这段在官网的原文中已经被删除:

因为.ajaxComplete()是作为一个jQuery对象实例方法去执行的,回调函数中,我们可以用this关键字作为指定的元素.



无论哪一个Ajax请求被发送,所有的ajaxSend处理器都将被执行.如果我们必须区分不同的请求,我们可以使参数传递给这个处理器. 每次ajaxSend处理器执行,它传递事件对象,jqXHR对象,(在jQuery 1.4中是XMLHttpRequest 对象) , 和用来创建请求的设置(settings object) 对象. 如果请求失败,因为JavaScript抛出一个异常,并且作为第四个参数的异常对象被传递给处理程序.举个实例,我们能限制我们的回调到只处理事件处理某一特定的URL:

```javascript
$(document).ajaxSend(function(event, jqxhr, settings) {
2.  if ( settings.url == "ajax/test.html" ) {
3.    $( ".log" ).text( "Triggered ajaxSend handler." );
4.  }
5.});
```

其他注意事项:

- 在jQuery1.9中,jQuery全局AJAX事件的所有处理程序,包括那些.ajaxSend()添加的方法,必须附加到document上.
- 如果$.ajax()或$.ajaxSetup()调用时,global选项设置为false, .ajaxSetup()将不会被触发.

## 示例

​	AJAX请求发送前显示信息

jQuery代码:

```javascript
$("#msg").ajaxSend(function(evt, request, settings){
2.   $(this).append("<li>开始请求: " + settings.url + "</li>");
3. });
```



# ajaxStart()

概述 .ajaxStart( handler() )

返回值: jQuery

## 描述: 在AJAX请求刚开始时执行一个处理函数,这是一个Ajax Event

​	.ajaxStart ( handler())

​		handler() 类型: Function() 被调用的函数

每当一个Ajax请求即将发送,jQuery检查是否由任何其他响应过程中的Ajax请求(注:未完成的请求) . 如果没有检查到.jQuery就会触发ajaxStart事件, 在这个时间点所有处理函数都会使用.ajaxStart()方法注册并执行

观察这种方法,建立一个基本的Ajax加载请求:

```html
<div class="trigger">Trigger</div>
2.<div class="result"></div>
3.<div class="log"></div>
```

在document上绑定事件处理器:

```javascript
$(document).ajaxSend(function() {
2.  $( ".log" ).text( "Triggered ajaxSend handler." );
3.});
```

现在,我们可以使用任何的jQuery方法构建一个Ajax请求:

```javascript
$( ".trigger" ).click(function() {
2.  $( ".result" ).load( "ajax/test.html" );
3.});
```

当我们点击class为trigger的元素 并且Ajax请求即将开始,这个信息就会显示.



# ajaxStop()



概述: .ajaxStop( handler() )

返回值: jQuery

描述: 在AJAX请求完成时执行一个处理函数. 这是一个Ajax Event.

.ajaxStop( handler() )

handler() 类型: Function() 被调用的函数

每当一个Ajax 请求完成,jQuery 检查是否有任何其他响应过程中的Ajax请求(未完成的请求) . 如果都执行完成,jQuery就会触发ajaxStop事件,在这个时间点所有处理函数都会使用.ajaxStop()方法注册并执行.如果一个未处理完的Ajax 请求用beforeSend()回调函数返回false取消, ajaxStop事件也被触发

观察这种方法,建立一个基本的 Ajax加载请求:

```javascript
<div class="trigger">Trigger</div>
<div class="result"></div>
<div class="log"></div>
```

在document上绑定事件处理器:

```javascript
$(document).ajaxSend(function() {
2.  $( ".log" ).text( "Triggered ajaxSend handler." );
3.});
```

现在, 我们可以使用任何的.jQuery方法构建一个Ajax请求:

```javascript
$( ".trigger" ).click(function() {
2.  $( ".result" ).load( "ajax/test.html" );
3.});
```

当我们点击class为trigger 的元素 并且Ajax 请求即将开始,这个信息就会显示

## 其他注意事项:

在jQuery 1.9中,jQuery全局AJAX事件的所有处理程序,包括哪些.ajaxStop()添加的方法,必须附加到document上.

如果$.ajax() 或 $.ajaxSetup()调用时, global选项设置为false, .ajaxStop()将不会触发.

实例

AJAX 请求结束后隐藏信息.

jQuery 代码: 

```javascript
 $("#loading").ajaxStop(function(){
2.   $(this).hide();
3. });
```



# ajaxSucces()

概述:

返回值: jQuery

描述: 绑定一个函数当Ajax请求成功完成时执行,这是一个 Ajax Event

.ajaxSuccess( handler (event, XMLHttpRequest, ajaxOptions ))

handler(event, XMLHttpRequest .ajaxOptions)

类型: Function()

被调用的函数.

每当一个Ajax请求完成,jQuery就会触发ajaxSuccess事件, 在这个时间点所有处理函数都会使用.ajaxSuccess 方法注册并执行

观察这种方法,建立一个基本的Ajax加载请求:

```javascript
<div class="trigger">Trigger</div>
2.<div class="result"></div>
3.<div class="log"></div>
```

在document上绑定事件处理器:

```javascript
$(document).ajaxSend(function() {
2.  $( ".log" ).text( "Triggered ajaxSend handler." );
3.});
```

现在,我们可以使用任何的jQuery方法构建一个Ajax请求:

```javascript
$( ".trigger" ).click(function() {
2.  $( ".result" ).load( "ajax/test.html" );
3.});
```

当我们点击class为 trigger 的元素并且Ajax请求即将开始,这个信息就会显示

无论哪一个Ajax请求被完成,所有ajaxSuccess 处理器都将被执行,如果我们必须区分不同的请求,我们可以使参数传递给这个处理器.他是通过事件对象, XMLHttpRequest 对象和设置对象中使用的请求,做每一次ajaxSuccess 处理器执行的. 举个示例,我们能限制我们的回调到只处理事件处理某一特定的URL:

```javascript
$(document).ajaxSuccess(function(event, xhr, settings) {
2.  if ( settings.url == "ajax/test.html" ) {
3.    $( ".log" ).text( "Triggered ajaxSuccess handler. The ajax response was: " +
4.                      xhr.responseText );
5.  }
6.});
```

注意: 你可以得到返回的AJAX内容 察看XML和HTML的xhr.responseXML或xhr.responseHTML 之间的分别.

## 其他注意事项:

在jQuery 1.9 中,jQuery全局AJAX事件的所有处理程序,包括哪些.ajaxSuccess()添加的方法,必须附加到document上

如果$.ajax() 或 $.ajaxSetup()调用时, global选项设置为false, .ajaxSuccess()将不会触发.

示例:

当AJAX请求成功后显示信息:

jQuery代码:

```javascript
 $("#msg").ajaxSuccess(function(evt, request, settings){
2.   $(this).append("<li>请求成功!</li>");
3. });
```



# jQuery.ajaxSetup()

返回值:jQuery

描述: 为以后用到的Ajax请求设置默认的值

jQuery.ajaxSetup( options )

options : 类型: PlainObject 一个用来配置 Ajax请求的"{键:值}" 对,所有的选项都是可选的.

用于设置$.ajaxSetup()的详细参数,参见 $.ajax()

所有后面的Ajax调用任何函数都将使用新的设置参数,除非它们调用时设置了各自的参数重载了这个默认值,直到下次调用$.ajaxSetup()

注意:此处指定的设置会影响所有 $.ajax或基于AJAX的衍生方法,如$.get()调用. 这可能会导致不良的行为,因为其他的调用(例如,插件)可能希望正常的默认设置. 出于这个原因,我们强烈建议您不要使用此API. 相反,我们建议,在调用时明确设置选项或定义一个简单的插件.

举个示例,我们可以事先设置服务器重复响应的默认URL参数:

```javascript
$.ajaxSetup({
  url: 'ping.php'
});
```

现在每次ajax请求将自动使用这个"ping.php" URL:

```javascript
$.ajax({
2.  // url not set here; uses ping.php
3.  data: {'name': 'Dan'}
4.});
```

注意:全局回调函数应使用它们各自的全局Ajax事件处理方法 - 

- .ajaxStart(), 
- .ajaxStop(), 
- .ajaxComplete(),
- .ajaxError(),
- .ajaxSuccess(),
- .ajaxSend(), 

​					- 设置, 而不是为$.ajaxSetup()设置options对象.

## 示例

设置AJAX请求默认地址为"/xmlhttp/" ,禁止触发全局AJAX事件,用POST代替默认GET方法,其后的AJAX请求不再设置任何选项参数.

jQuery代码:

```javascript
$.ajaxSetup({
2.  url: "/xmlhttp/",
3.  global: false,
4.  type: "POST"
5.});
6.$.ajax({ data: myData });
```



# jQuery.ajaxTransport()



概述 jQuery.ajaxTransport(dataType , handler(options, originalOptions, jqXHR))

描述: 创建一个对象,用于处理Ajax数据的实际传输

jQuery.ajaxTransport( dataType, handler(options , originalOptions, jqXHR))

​		dataType 类型: String 一个字符串,标识使用的数据类型

​		handler( options, originalOptions, jqXHR)

​		类型: Function() 一个处理程序,使用第一个参数中提供的数据类型返回新的传输( transport ) 对象.

传输( transport )是一个对象,它提供了两种方法, send和 abort ,内部使用$.ajax()发出请求. 传输( transport )是最高级的方法用来增强$.ajax()并且应仅作为当预过滤器 (prefilters) 和转换器( converters ) 无法满足你的需求的时候的最后手段

由于每个请求需要有自己的传输(transport)对象实例,传输不能直接注册.因此,你应该提供一个函数代替返回传输 ( transport )

传输 (transports) 工厂注册使用$.ajaxTransport(). 一个典型的注册看起来像这样:

```javascript
$.ajaxTransport( dataType, function( options, originalOptions, jqXHR ) {
2.  if( /* transportCanHandleRequest */ ) {
3.    return {
4.      send: function( headers, completeCallback ) {
5.        // Send code
6.      },
7.      abort: function() {
8.        // Abort code
9.      }
10.    };
11.  }
12.});
```

以下的情况下:

- options 是请求的选项
- originalOptions 值作为提供给 Ajax方法未经修改的选项,因此,没有ajaxSettings 设置中的默认值
- jqXHR是请求的jqXHR对象
- headers 是一个请求头信息(键-值) 对象, 该传输( transport ) 都可以发送,如果它支持
- completeCallback 是回调用于该请求Ajax的完成通知

completeCallback 具有以下签名:

function (status,statuaText, responses,headers){}

以下的情况下:

- status是响应的HTTP状态代码,像200 是一个典型的成功,或404是没有找到资源

- statusText 是响应状态文本.

- responses(可选)是一个对象,它包含数据类型/值( dataType/value )包含响应运输提供的所有格式.

  (例如, 一个原生的XMLHttpRequest 对象设置responses为{ xml:XMLData, text:textData }) ,这样响应是一个XML文档

- headers (可选) 是一个字符串,其中包含所有的响应信息头,如果运输对它们的访问(类似于XMLHttpRequest.getAllResponseHeaders()提供的方法.

就像预过滤器( prefilters ) 一个传输( transport )的工厂函数可以被连接到一个特定的dataType(数据类型):

```javascript
$.ajaxTransport( "script", function( options, originalOptions, jqXHR ) {
2.    /* Will only be called for script requests */
3.});
```

下面的示例演示小的图像怎样传输实现

```javascript
$.ajaxTransport( "image", function( s ) {
2. 
3.  if ( s.type === "GET" && s.async ) {
4. 
5.    var image;
6. 
7.    return {
8. 
9.      send: function( _ , callback ) {
10. 
11.        image = new Image();
12. 
13.        function done( status ) {
14.          if ( image ) {
15.            var statusText = ( status == 200 ) ? "success" : "error",
16.            tmp = image;
17.            image = image.onreadystatechange = image.onerror = image.onload = null;
18.            callback( status, statusText, { image: tmp } );
19.          }
20.        }
21. 
22.        image.onreadystatechange = image.onload = function() {
23.          done( 200 );
24.        };
25.        image.onerror = function() {
26.          done( 404 );
27.        };
28. 
29.        image.src = s.url;
30.      },
31. 
32.      abort: function() {
33.        if ( image ) {
34.          image = image.onreadystatechange = image.onerror = image.onload = null;
35.        }
36.      }
37.    };
38.  }
39.});
```



## Handling Custom Data Types (处理自定义数据类型)

jQuery的 Ajax实现了一套标准的数据类型,比如text,json,xml,和html.

在$.ajaxSetup()中使用converters选项来增加或修改数据类型使用 $.ajax()转换策略

未更改的jQuery代码本身包含一个列表的默认转换器,这有力地说明了可以如何使用它们:

```javascript
1.// List of data converters
2.// 1) key format is "source_type destination_type"
3.//    (a single space in-between)
4.// 2) the catchall symbol "*" can be used for source_type
5.converters: {
6. 
7.  // Convert anything to text
8.  "* text": window.String,
9. 
10.  // Text to html (true = no transformation)
11.  "text html": true,
12. 
13.  // Evaluate text as a json expression
14.  "text json": jQuery.parseJSON,
15. 
16.  // Parse text as xml
17.  "text xml": jQuery.parseXML
18.}
```



当你在$.ajaxSetup()全局的指定一个converters选项, 或者每次调用$.ajax(),这个对象将映射到默认的转换器,覆盖您所指定的那些,让其他不变.

例如.jQuery代码使用$.ajaxSetup()添加一个" text script "转换器:

```javascript
jQuery.ajaxSetup({
2.  accepts: {
3.    script: "text/javascript, application/javascript"
4.  },
5.  contents: {
6.    script: /javascript/
7.  },
8.  converters: {
9.    "text script": jQuery.globalEval
10.  }
11.});
```



# jQuery.get()

概述 jQuery.get(url [.data ] [,success ] [,dataType])

返回值: XMLHttpRequest

描述: 使用一个HTTP GET请求从服务器加载数据

jQuery.get(url [,data ] [,success ] [,dataType ])

​	url: 类型 String 一个包含发送请求的字符串

​	data 类型: PlainObject or String 一个普通对象或字符串 ,通过请求发送给服务器

​	success 类型: Function( PlainObject data, String textStatus, jaXHR jqXHR)

​	dataType  类型 : String 从服务器返回的预期的数据类型. 默认: 只能猜测( xml , json ,script ,text, html ).

jQuery.get( [ settings ] )

​	settings 

​	类型: PlainObject 

​	一组用于配置Ajax请求的键/值对. 除了url意外的所有选项属性都是可选的, 任何默认选项可以用$.ajaxSetup()进行设置. 所有选项设置的完整列表,请参阅jQuery.ajax( settings ). type (类型)选项自动设置为GET.

这是一个Ajax功能的缩写,这相当于:

```javascript
$.ajax({
 url: url,
 data: data,
  success: success,
  data类型:dataType
});
```

success 回调函数会传入返回的数据,是根据MIME类型的响应,它可能返回的数据类型包括XML根节点,字符串,JavaScript 文件, 或者JSON对象,同时 还会传入描述响应状态的字符串

在jQuery1.5 ,success 回调函数还传递一个"jqXHR" 对象(在jQuery 1.4中,它传递的是XMLHttpRequest 对象). 然而,由于JSONP形式和跨域的GET请求不使用XHR,在这些情况下,jaXHR和textStatus 参数传递给success 回调是undefined

大多数实现将指定一个成功的回调处理程序:

```javascript
$.get('ajax/test.html', function(data) {
2.  $('.result').html(data);
3.  alert('Load was performed.');
4.});
```

这个示例所请求到的HTML代码片段插在页面中

## The jqXHR Object 

从jQuery1.5开始,所有jQuery的Ajax方法都返回一个XMLHttpRequest 对象的超集. 这个通过$.get()方法返回的jQuery XHR对象,或"jqXHR" , 实现了 Promise接口,使它拥有Promise的所有属性,方法和行为 jqXHR.done()表示成共,jqXHR.fail()(表示错误) , 和jqXHR.always()(表示成功,无论是成功或错误; 在1.6中添加) 方法接受一个函数参数,用来请求终止时被调用.关于这个函数接受参数的详细信息,请参阅jqXHR Object 文档中的$.ajax()章节.

Promise 接口也允许jQuery的Ajax方法,包括$.get(), 在一个单独的请求中关联到 .done(), .fail(), 和 .always()回调函数, 甚至允许你在请求结束后,指派回调函数.如果该请求已经完成,则回调函数会被立刻调用.

```javascript
// Assign handlers immediately after making the request,
2.  // and remember the jqxhr object for this request
3.  var jqxhr = $.get("example.php", function() {
4.    alert("success");
5.  })
6.  .success(function() { alert("second success"); })
7.  .error(function() { alert("error"); })
8.  .complete(function() { alert("complete"); });
9. 
10.  // perform other work here ...
11. 
12.  // Set another completion function for the request above
13.  jqxhr.complete(function(){ alert("second complete"); });
```



示例:

请求test.php页面,但是忽略返回结果:

```javascript
$.get("test.php");
```

示例:

请求test.php页面,并且发送url 参数(虽然仍然忽视返回的结果)

```javascript
$.get("test.php", { name: "John", time: "2pm" } );
```

示例

传递数组形式data参数给服务器,(虽然仍然忽视返回的结果)

```javascript
$.get("test.php", { 'choices[]': ["Jon", "Susan"]} );
```

示例

Alert 从test.php 请求的数据结果 (HTML 或者 XML取决于返回的结果)

```javascript
$.get("test.php", function(data){
2.    alert("Data Loaded: " + data);
3.});
```

示例

Alert 从 test.cgi 请求并且发送url参数的数据结果 (HTML 或者 XML 取决于返回的结果)

```javascript
$.get("test.cgi", { name: "John", time: "2pm" },
2.   function(data){
3.     alert("Data Loaded: " + data);
4.});
```

示例

获取test.php 的页面已返回的JSON格式的内容 (<?php echo json_encode(array("name=>"john","time"=>"2pm"; ))?>), 并且加到页面中

```javascript
$.get("test.php",
2.   function(data){
3.     $('body').append( "Name: " + data.name ) // John
4.              .append( "Time: " + data.time ); //  2pm
5.   }, "json");
```



# jQuery.getJSON()

概述  jQuery.getJSON( url [,data] [,success(data,textStatus,jqXHR) ])

返回值: XMLHttpRequest 

描述: 使用一个HTTP GET请求从服务器加载JSON编码的数据

jQuery.getJSON(url [,data ] [,success(data, textStatus,jqXHR )])

​	url 类型: String 一个包含发送请求的URL字符串

​	data 类型: PlainObject or String 一个普通的对象或字符串,用来发送请求给服务器

​	success 类型: Function( PlainObject data, String textStatus, jqXHR jqXHR) 当请求成功后执行的回调函数

这是一个 Ajax函数的缩写,这相当于:

```javascript
1.$.ajax({
2.  dataType: "json",
3.  url: url,
4.  data: data,
5.  success: success
6.});
```

