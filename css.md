overflow: auto 可以把溢到元素外部的元素收回来，当然会在元素内产生滚动条

所有的元素都默认没有高度，需要子元素撑起来

p标签内只能是行内元素或者文本字段，不能是块级元素。如果出现块级元素浏览器会把代码自动解析成这样：

​		

```html
<p></p>
	<h3></h3>
<p></p>
```

​		本来应该是这样:

```html
<p>
	<h3></h3>
</p>
```

​		除了<p>之外，下面几个特殊的块级元素只能包含内嵌元素，不能再包含块级元素：

<h1-6>,<dt>

设置input和button组和水平对齐：

```css
input,button{
	vertical-align:top;
}
```

设置input和button同样高度值，但却不能等高的原因：

1. button在高度计算上始终使用了Quirks模式。

2. 在Quirks模式下，边框的计算是在元素的宽度内的，而不像标准模式一样计算在外部，所以在text和button上同时设置边框就会得到button的高度比text小的现象。

3. button的高度包含边框的高度，而文本框text则不包含边框高度。

   解决方法：将边框都设置为none;

   ```css
   <style>
           .text{
               height: 45px;
               width: 180px;
               background: yellow;
               border: none;
           }
           .button{
               height: 45px;
               width: 90px;
               background: red;
               border: none;
           }
    </style>
   ```

   

## 区分块级元素和内联元素：

​		简单介绍一些内联和块级元素最直白的区别：block元素往往是独占一行的。inline元素的高度和广度是由自己的内容		填充的。所以看看这两个元素的表现形式就可以区分出来他们是什么类型的元素了。如果还区分不出来，按F12查看		计算后的样式，由display一项。根据这一项就可以确定它是什么类型的元素了。

​		<a>和 br 都是不会独占一行的。我认为应该属于inline元素。

判断的标准由两个：

1. 是否独占一行。

2. 是否可以单独为元素设置高度和宽度

   内联元素的两个答案都是否。

去除chrome等浏览器文本框默认发光边框：

```css
input:focus, textarea:focus {

    outline: none;

}
```

## 实现input内的光标右移：

```css
input{
	padding-left:20px;
}
```

