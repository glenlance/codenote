var : 是函数作用域 , function scope

let / const  : 是块级作用域, block scope

let / const 不能在同一个作用域重复声明一个变量

临时性死区:

![](C:\Users\y5039\Pictures\Camera Roll\Annotation 2019-06-08 175929.png)

- use const by default
- only use let if rebinding is needed
- (var shouldn't be used in ES6)

let声明的变量只在其声明的块或子块中可用,这一点,与var相似. 二者之间最主要的区别在于var声明的变量的作用域是整个封闭函数.

# js中的this是在运行时才绑定的.

# 箭头函数没有自己的this值, 它的this值是继承它自己的父作用域的.

# 箭头函数的作用域是词法作用域



# 当你要定义一个对象上的原型方法时, 不宜使用箭头函数



## 什么时候不要使用箭头函数 ?

1. 作为构造函数,一个方法需要绑定到对象
2. 当你真正需要this的时候
3. 需要使用arguments对象







