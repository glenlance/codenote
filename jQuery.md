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
    [ jQuery对象其实是一个伪数组。]
    
        什么是伪数组: 有0-length-1的属性，并且有length属性


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