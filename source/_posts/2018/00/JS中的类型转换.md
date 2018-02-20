---
title: JS中的类型转换
date: 2017-05-23 22:41:31
categories: 前端
tags:
    - JavaScript
    - 类型转换
    - 运算符
    - ECMA
---

|        值         |   转字符串  | 数字 | 布尔值 |          对象         |
| :---------------: | :---------: | :--: | :----: | :-------------------: |
|     undefined     | 'undefined' |  0   | false  |    throws TypeError   |
|        null       |    'null'   |  0   | false  |    throws TypeError   |
|        true       |    'true'   |      1       ||   new Boolean(true)   |
|       false       |   'false'   |      0       ||   new Boolean(false)  |
|   '' (空字符串)   |             |  0   | false  |     new String('')    |
| '1.2'(数字字符串) |             | 1.2  |  true  |   new String('1.2')   |
|     'shiny'(非数字字符串)      || NaN  |  true  |  new String('shiny')  |
|         0         |     '0'     |      | false  |     new Number(0)     |
|         -0        |     '0'     |      | false  |     new Number(-0)    |
|      Infinity     |  'Infinity' |      |  true  |  new Number(Infinity) |
|     -Infinity     | '-Infinity' |      |  true  | new Number(-Infinity) |
|         33        |     '33'    |      |  true  |     new Number(33)    |
|   {} (任意对象)   |             |      |  true  |    new Number(NaN)    |
|         []        |      ''     |  0   |  true  |    new Number(NaN)    |
|        [33]       |     '33'    |  33  |  true  |    new Number(NaN)    |
|       ['a']       |     'a'     | NaN  |  true  |    new Number(NaN)    |
|    function(){}   |             | NaN  |  true  |    new Number(NaN)    |
- 原始值转对象很简单，原始值通过调用String()，Number()，Boolean()构造函数，转换为他们各自的包装对象。`null`和`undefined`属于例外，当将他们用在期望是一个对象的地方都会造成一个类型错误(TypeErroe)异常，而不会执行正常的转换。
- 对象转换相对复杂，下面具体描述

<!-- more -->

### 转换和相等性
由于JS可以做灵活的类型转换，因此其`==`相等运算符也随相等的含义灵活多变。例如：
```js
null == undefined       // 这两值被认为相等
'0'  == 0               // 前面的字符串转为了数字
 0   == false           // 比较之前布尔值转成了数字
'0'  == false           // 比较前字符串和布尔值都转成了数字
```
`==`一个值转换为另一个值并不意味着两个值相等。比如，如果在期望使用布尔值的地方使用了undefined，它将会转换为false，但这并不表明`undefined == false`。
**JS运算符和语句期望使用多样化的数据类型，并可以相互转换。if语句将undefined转换为false，但`==`运算符从不试图将其操作数转换为布尔值。**
> 相等运算符`==`比较并不严格。如果两个操作数不是同一类型，那么相等运算符会尝试进行一些类型转换，然后进行比较：

- 如果两个操作数的类型相同，则根据值进行比较，也就是类似于严格相等(`===`)进行比较。
- 如果两个操作数类型不同，`==`相等操作符也可能会认为他们相等。检测相等将会遵守如下规则和类型转换：
1、如果一个值是null，另一个是undefined，则它们相等。
2、如果一个值是数字，另一个是字符串，先将字符串转换为数字，然后使用转换后的值进行比较。
3、如果其中一个值是true，则将其转为1再进行比较。如果其中一个值是false，则将其转换为0再进行比较。
4、如果一个值是对象，另一个值是数字或字符串，则将对象转为原始值，然后再进行比较。对象通过toString()方法或者valueOf()方法转换为原始值。JS语言核心的内置首先尝试使用valueOf()，再尝试使用toString()，除了日期类，日期类只是用toString()转换。那些不是JS语言核心中的对象则通过各自的实现中定义的方法转换为原始值。
5、其他不同类型之间的比较均不相等。

### 显示类型转换
- 做显示类型转换最简单的方法就是使用Boolean()、Number()、String()或Object()函数。当不通过new运算符调用这些函数时，它们会作为类型转换函数：
```js
Number('3')         // => 3
String(false)       // => 'false'
Boolean([])         // => true
Object(3)           // => new Number(3)
```
需要注意的是，除了null或undefined之外的任何值都具有toString()方法，这个方法执行结果通常和String()方法的返回结果一致。
- JS中某些运算符会做隐式的类型转换，又是用户类型转换。
```js
x+''            // 等价于String('x')
+x              // 等价于Number(x).也可以写成x-0
!!x             // 等价于Boolean(x).注意是双叹号。
10+'shiny'      // '10shiny',数字10转换为字符串
'7'*'4'         // 28，两个字符串均转换为数字
var n = 1 - 'x' // NaN: 字符串x无法转换为数字
n + 'shiny'     // 'NaN shiny': NaN转换为字符串NaN
```
- Number类定义的toString()方法可以接收表示转换基数(radix)的可选参数，如果不指定此参数，转换规则将是基于十进制。
```js
var n = 17;
var a = n.toString(2);          // 转化为 ‘10001’
var b = '0' + n.toString(8);    // 转换为‘021’
var c = '0x' + n.toString(16);  // 转换为‘0x11'
```
- 如果通过Number()转换函数传入一个字符串，它会试图将其转化为一个整数或浮点数直接量，这个方法只能基于十进制数进行转换，并且不能出现非法的尾随字符。parseInt()函数和parseFloat()函数（它们是全局函数，不从属于任何类的方法）更加灵活。parseInt()可以接收第二个可选参数，这个参数指定数字转换的基数，合法的取值范围是2-36。
```js
parseInt('1 shinygang')          // => 3
parseFloat('3.14 shinygang')     // => 3.14
parseInt('-12.33')               // => -12
parseInt('0xff')                 // => 255
parseFloat('.1')                 // => 0.1
parseInt('.1')                   // => NaN，整数不能以'.'开始
parseInt('11', 2)                // => 3 (1*2+1)
parseInt('ff', 16)               // => 255 (15*16+15)
```

### 对象转换为原始值
- 对象到布尔值的转换非常简单：所有对象(包括数组和函数)都转换为true。对于包装对象亦是如此：new Boolean(false)是一个对象而不是原始值，它江转换为true。
- 对象到字符串和对象到数字的转换都是通过调用带转换对象的一个方法来完成的。JS对象有两个不同的方法来执行转换：toString()和valueOf()
**toString():**它的作用是返回一个反应这个对象的字符串。默认的toString()方法并不会返回一个有趣的值。
```js
({x:1}).toString()      // => "[object Object]"
```
很多类定义了更多特定版本的toString()方法。例如，数组类的toString()方法将每个数组元素转换为一个字符串，并在元素之间添加逗号后合并成结果字符串。函数类的toString()方法返回这个函数的实现定义表示方式。日期类定义的toString()方法返回了一个可读的日期和时间字符串。RegExp类定义的toString()方法将RegExp对象转换为表示正则表达式直接量的字符串。
```js
[1,2,3].toString()                  // => "1,2,3"
(function(x){f(x);}).toString()     // => "function(x){\n f(x); \n}"
/\d/g.toString()                    // => "/\\d/g"
new Date(2010,0,1).toString()       // => "Fri Jan 01 2010 00:00:00 GMT+0800 (CST)"
```
**valueOf():**如果存在任意原始值，它就默认将对象转换为表示它的原始值。对象是复合值，而且大多数对象无法真正表示为一个原始值，因此默认valueOf()方法简单地返回对象本身，而不是返回一个原始值。数组、函数和正则表达式简单地继承了这个默认方法，调用这些类型的实例的valueOf()方法只是简单返回对象本身。日期则返回对应毫秒数。
3..1、JS中对象到字符串的转换经过了如下这些步骤：
* 如果对象具有toString()方法，则调用这个方法。如果他返回一个原始值，JS将这个原始值转换为字符串，并返回这个字符串结果。
* 如果对象没有toString()方法，或这个方法并不返回一个原始值，那么JS会调用valueOf()方法。如果存在这个方法，则JS调用它。如果返回值是原始值，JS将这个值转换为字符串，并返回这个字符串结果。
* 否则，JS无法从toString()或valueOf()获得一个原始值，因此这时它将抛出一个类型错误异常。
3.2、在对象到数字的转换过程中，JS做了同样的事情，只是它会首先尝试使用valueOf()方法：
* 如果对象具有valueOf()方法，后者返回一个原始值，则JS将这个原始值转换为数字返回
* 否则，如果对象具有toString()方法，返回一个原始值，则JS将其转换并返回
* 否则，JS抛出一个类型异常错误。
