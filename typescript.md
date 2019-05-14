## 内置对象

JavaScript 中有很多[内置对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)，它们可以直接在 TypeScript 中当做定义好了的类型。

内置对象是指根据标准在全局作用域（Global）上存在的对象。这里的标准是指 ECMAScript 和其他环境（比如 DOM）的标准。

ECMAScript 的内置对象

ECMAScript 标准提供的内置对象有：

## 标准内置对象的分类

## 指属性:

这些全局属性返回一个简单值，这些值没有自己的属性和方法。

- [`Infinity`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Infinity)
- [`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)
- [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined)
- [`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null) 字面量

## 函数属性

全局函数可以直接调用，不需要在调用时指定所属对象，执行结束后会将结果直接返回给调用者。

- [`eval()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/eval)
- [`uneval()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/uneval) 
- [`isFinite()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/isFinite)
- [`isNaN()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/isNaN)
- [`parseFloat()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)
- [`parseInt()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)
- [`decodeURI()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/decodeURI)
- [`decodeURIComponent()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/decodeURIComponent)
- [`encodeURI()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/encodeURI)
- [`encodeURIComponent()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)

## 基本对象

顾名思义，基本对象是定义或使用其他对象的基础。基本对象包括一般对象、函数对象和错误对象。

- [`Object`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)
- [`Function`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Function)
- [`Boolean`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Boolean)
- [`Symbol`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol)
- [`Error`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Error)
- [`EvalError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/EvalError)
- [`InternalError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/InternalError)
- [`RangeError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RangeError)
- [`ReferenceError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ReferenceError)
- [`SyntaxError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/SyntaxError)
- [`TypeError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/TypeError)
- [`URIError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/URIError) 

## 数字和日期对象

用来表示数字,日期和执行数学计算的对象.

- [`Number`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number)
- [`Math`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math)
- [`Date`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Date) 

## 字符串

用来表示和操作字符串的对象.

- String
- RegExp

## 可索引的集合对象

这些对象表示按照索引值来排序的数据集合,包括数组和类型数组,以及类数组结构的对象.

- [`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array)
- [`Int8Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Int8Array)
- [`Uint8Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array)
- [`Uint8ClampedArray`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Uint8ClampedArray)
- [`Int16Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Int16Array)
- [`Uint16Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Uint16Array)
- [`Int32Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Int32Array)
- [`Uint32Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Uint32Array)
- [`Float32Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Float32Array)
- [`Float64Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Float64Array) 

## 使用键的集合对象

这些集合对象在存储数据时会使用到键,支持按照插入顺序来迭代元素.

- Map
- Set
- WeakMap
- WeakSet

## 矢量集合

SIMD 矢量集合中的数据会被组织为一个数据序列.( 都是实验性的API,不要在生产环境中使用 )

- 
- [`SIMD`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/SIMD) 
- [`SIMD.Float32x4`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Float32x4) 
- [`SIMD.Float64x2`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Float64x2) 
- [`SIMD.Int8x16`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Int8x16) 
- [`SIMD.Int16x8`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Int16x8) 
- [`SIMD.Int32x4`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Int32x4) 
- [`SIMD.Uint8x16`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Uint8x16) 
- [`SIMD.Uint16x8`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Uint16x8) 
- [`SIMD.Uint32x4`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Uint32x4) 
- [`SIMD.Bool8x16`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Bool8x16) 
- [`SIMD.Bool16x8`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Bool16x8) 
- [`SIMD.Bool32x4`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Bool32x4) 
- [`SIMD.Bool64x2`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Bool64x2) 

##   结构化数据

这些对象用来表示和操作结构化的缓冲区数据,或使用JSON( JavaScript Object Notation )编码的数据.

- ArrayBuffer
- ShareArrayBuffer
- Atomics
- DataView
- JSON

## 控制抽象对象

- Promise
- Generator
- GeneratorFunction

## 反射

- Reflect
- Proxy

## 国际化

为了支持多语言处理而加入ECMAScript的对象。

- Intl
- Intl.Collator
- Intl.DataTImeFormat
- Intl.NumberFormat

## WebAssembly

- [`WebAssembly`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/WebAssembly)
- [`WebAssembly.Module`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/WebAssembly/Module)
- [`WebAssembly.Instance`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/WebAssembly/Instance)
- [`WebAssembly.Memory`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/WebAssembly/Memory)
- [`WebAssembly.Table`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/WebAssembly/Table)
- [`WebAssembly.CompileError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/WebAssembly/CompileError)
- [`WebAssembly.LinkError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/WebAssembly/LinkError)
- [`WebAssembly.RuntimeError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/WebAssembly/RuntimeError) 

## 其他

- arguments

## DOM和BOM的内置对象

DOM和BOM提供的内置对象有:

Document,HTMLElement,Event,NodeList 等.

他们的定义文件在TypeScript核心库的定义文件中.

TypeScript核心库的定义文件中定义了所有浏览器环境需要用到的类型,并且时预置在TypeScript中的.

当你在使用一些常用的方法的时候,TypeScript实际上已经帮你做了很多类型判断的工作了,比如:

```typescript
Math.pow(10, '2');

// index.ts(1,14): error TS2345: Argument of type 'string' is not assignable to parameter of type 'number'.
```

上面的例子中，`Math.pow` 必须接受两个 `number` 类型的参数。事实上 `Math.pow` 的类型定义如下：

```typescript
interface Math {
    /**
     * Returns the value of a base expression taken to a specified power.
     * @param x The base value of the expression.
     * @param y The exponent value of the expression.
     */
    pow(x: number, y: number): number;
}
```

再举一个 DOM 中的例子：

```typescript
document.addEventListener('click', function(e) {
    console.log(e.targetCurrent);
});

// index.ts(2,17): error TS2339: Property 'targetCurrent' does not exist on type 'MouseEvent'.
```

上面的例子中，`addEventListener` 方法是在 TypeScript 核心库中定义的：

```typescript
interface Document extends Node, GlobalEventHandlers, NodeSelector, DocumentEvent {
    addEventListener(type: string, listener: (ev: MouseEvent) => any, useCapture?: boolean): void;
}
```

所以 `e` 被推断成了 `MouseEvent`，而 `MouseEvent` 是没有 `targetCurrent` 属性的，所以报错了。

注意，TypeScript 核心库的定义中不包含 Node.js 部分。

## 用Typescript写Node.js

Node.js不是内置对象的一部分,如果想用TypeScript写Node.js 则需要引入第三方声明文件:

```
npm install @types/node --save-dev
```



## Node节点对象 和 Element 对象的区别

NodeList只是一个类似数组的节点列表.

ELEMENT_NODE是nodeType属性的值为1的一种特定类型的节点。

由于document.getElementsByClassName(“para”)可以返回多个对象，设计者选择返回一个nodeList，因为这是他们为多个节点的列表创建的数据类型.