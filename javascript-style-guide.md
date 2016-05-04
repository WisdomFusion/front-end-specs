# JavaScript Style Guide - JavaScript 开发规范

## 简介

为了有效提高代码的质量，基于“易维护、易调试、高性能”的原则，参考业界知名团队的规范与指南制订本规范，大家在编写 JavaScript 代码时，应尽量遵守本规范，提高自己的代码质量。

## 命名

JavaScript 是区分大小写的语言，在对 JavaScript 种的变量、函数、常量等命名时，应该遵循 JavaScript 自身采用的命名规则，以保持代码的一致性。具体规则如下：

**常量**

JavaScript 自身不支持常量，在程序中如果要定义“禁止定义后改变”的变量，可以参考其他编程语言，采用下划线分隔的全大写字符串来定义。例如：LINE_SEPORATOR 等。

**变量**

首字母小写，驼峰命名法，原则上采用名词及名词短语，描述该变量代表的数据。例如：`btnSubmit`、`frmLoginForm`。

**函数**

首字母小写、驼峰命名法，原则上函数采用动词及动词短语，以描述该函数的行为，对象采用名词及名词词组。例如：`login()`、`checkLogin()`、`showVideo()`、`switchTabs()`、`changeLevel()`、`addClass()`、`loadScript()`。

**类及命名空间**

首字母大写、驼峰命名法。例如：LoginManager、UserInfo、RoleManager。

**文件名**

全小写、单词间可以不分隔或用连接线 `-` 分隔，文件名可以加 `.min` / `.debug` 表示文件状态，例如：common.js（一般的文件名）、base.min.js (压缩后的文件)、common.debug.js (未压缩、调试用的文件)。

**可读性**

在未做压缩处理的源代码中，类、变量、函数的命名应该尽量具有语义，应当避免 `a`、`b`、`xyz` 这类无意义的命名（循环语句中的 i/j/k 等习惯用法除外）。代码的压缩，应该采用专门的工具（如 YUI Compressor、Google Closure）来进行，不要人为用无意义的命名来减少代码量。

## 变量的定义和初始化

JavaScript 并不强调变量在使用前必须定义。但是如果没有使用 `var` 关键字来定义变量，则该变量将会成为全局变量。有可能会造成对同名全局变量的覆盖，在多人协作开发、引入多个库或多个 JavaScript 文件的情况下，容易导致变量名冲突等问题。因此，对变量的定义和初始化建议参照以下规则：

总是将代码包裹成一个 IIFE (Immediately-Invoked Function Expression)，用以创建独立隔绝的定义域。这一举措可防止全局命名空间被污染。IIFE 还可确保你的代码不会轻易被其它全局命名空间里的代码所修改（如，第三方库，window 引用，被覆盖的未定义的关键字等等）。

```javascript
// 不推荐

var x = 10,
    y = 100;
 
// Declaring variables in the global scope is resulting in global scope pollution. All variables declared like this
// will be stored in the window object. This is very unclean and needs to be avoided.
console.log(window.x + ' ' + window.y);

// 推荐

// We declare a IIFE and pass parameters into the function that we will use from the global space
(function(log, w, undefined){
  'use strict';
 
  var x = 10,
      y = 100;
 
  // Will output 'true true'
  log((w.x === undefined) + ' ' + (w.y === undefined));
 
}(window.console.log, window));
```

虽然 JavaScript 是一门弱类型语言，变量的数据类型可以随时自由转换，但是在实际使用中，依然建议大家避免用同一个变量存储不同类型的数据。 在定义变量的同时对其初始化是很好的编程实践，这可以避免后续忘记给变量赋值而直接使用它引发的 "undefined" 错误。

## 代码风格

**大括号**

前大括号始终位于当前行末尾，后大括号新起一行并与代码块的首行保持相同缩进对齐，数组和对象的快速定义可以例外。例如，数组和对象的快速定义:

```javascript
var arr = [1, 2, 3];
var obj = {a: 1, b: 2, c: 3};
```

**数组初始化**

```javascript
this.rows = [
    'Tom',
    'Jerry',
    'Woo',
];
```

**函数调用中**

```javascript
tvp.play('u1134234422','mod_player', {
    autoplay: '1',
    width: 600,
    height: 449,
    controls: '1'
});
```

**函数定义**

```javascript
function functionName() {
    // function codes
}
```

**代码块**

```javascript
if (condition == true) {
    // do something
} else {
    // do something else
}
 
for(var i = 0; i < data.length; i++) {
    // loop body
}
```

```javascript
/* 不推荐 */
if(event.target)
    return event.target;
else
    return event.srcElement;

/* 推荐 */
if(event.target) {
    return event.target;
} else {
    return event.srcElement;
}
```

**注意：**对于代码块，始终用大括号包裹，对于单行判断、while 循环等可以省略大括号的，一律不省略。

**引号**

在处理字符串时，优先使用单引号，仅在必须的情况下才使用双引号。这不仅能保持代码的一致性、缩小代码文件大小，在创建包含HTML代码的字符串时，这尤其有利，例如：

```javascript
var msg = '<li class="msg">提示信息</li>';
```

**分号**

所有的语句必须用分号结尾。

```javascript
/* 不推荐 */
 
// 例1.
MyClass.prototype.myMethod = function() {
  return 42;
}  // 缺少分号
 
(function() {
  // some code
})();
 
// 例2.
var x = {
  'i': 1,
  'j': 2
}  // 缺少分号
 
[normalVersion, ffVersion][isIE]();
 
// 例3.
var THINGS_TO_EAT = [apples, oysters, sprayOnCheese]  // 缺少分号.
 
-1 == resultOfOperation() || die();
```

这样写会造成什么后果？ 

* 例1：JavaScript 错误 - 首先，原本是定义一个返回42的函数，变成了立即执行，并且把第二个函数当成了调用第一个函数的参数，然后42这个数字被当成一个函数返回并被调用，引发了错误。

* 例2：你最有可能看到的是代码执行的时候报“no such property in undefined”的错误，因为它会尝试执行x[ffVersion]isIE，而x[ffVersion]是未定义的。

* 例3：函数die()只有在resultOfOperation()的结果不为数字的时候才会被执行（预期是不为-1就执行），而THINGSTOEAT则被赋值为die()的执行结果（原本应该是个数组）。

为什么会这样呢？

JavaScript 要求语句以分号结束，除非解析器可以安全地分析出语句在哪里结束（例如定义函数时结尾的大括号）。在上面的错误范例中，由于函数定义、对象或数组被用在了语句当中，于是结束括号并不足以标识出语句的结尾。于是当下一个标识符可以作为语句的中间部分时（比如例子的中前括号、前中括号、-1等）JavaScript解析器就不会在我们预期的地方结束语句。 因此，不要试图依赖JavaScript解析器来为你“断句”，务必在需要结束语句的地方使用分号明确指出该语句已经结束。

```javascript
/* 推荐 */
 
var foo = function() {
  return true;
};  // 正确的结束分号.
 
function foo() {
  return true;
}  // 这里不要加分号.
 
if (condition) {
    // do something.
}  // 这里不要加分号
 
milo.addEvent(g('domId'), 'click', function(){
    // do something
}); // 正确的结束分号
 
(function(){
    function clickHandler(hotTag) {
        pgvSendClick({hottag:hotTag});
    }  // 这里不要分号
    var btn = document.getElementById('btnDown');
    btnDown.innerHTML = '下载';
    btnDown.click = function() {
      clickHandler('index.btnDown.client.xf');
    };  // 正确的结束分号
})();  // 正确的结束分号
```

**注释**

对代码中的类、方法、属性、复杂的实现逻辑等，应该加上必要的注释。注释的格式参照 JSDoc 语法。常见的注释范例：

```javascript
/**
 * 这是一段常规注释，不包含调用参数和返回值
 */
function doSomething() {
    alert('hello');
}
 
/**
 * 这是一个有调用参数和返回值的函数
 * 注释里要用@param和@return分别标注参数和返回值
 *
 * @param {number} index 每次执行时当前元素在数组中的索引
 * @param {object} dom 当前循环到的元素
 * @return {string} 每次循环时返回当前元素的id
 */
$.each = function(index, dom) {
    if(dom = this[index]) {
        return dom.id;
    } else {
        return '';
    }
};
```

## 技巧和实践

**eval 函数（魔鬼）**

`eval()` 不但混淆语境还很危险，总会有比这更好、更清晰、更安全的另一种方案来写你的代码，因此尽量不要使用 eval 函数。

**this 关键字**

只在对象构造器、方法和在设定的闭包中使用 `this` 关键字。 `this` 的语义在此有些误导。它时而指向全局对象（大多数时），时而指向调用者的定义域（在 eval 中），时而指向 DOM 树中的某一节点（当用事件处理绑定到 HTML 属性上时），时而指向一个新创建的对象（在构造器中），还时而指向其它的一些对象（如果函数被 `call()` 和 `apply()` 执行和调用时）。

正因为它是如此容易地被搞错，请限制它的使用场景：

* 在构造函数中
* 在对象的方法中（包括由此创建出的闭包内）

**True 和 False 布尔值表达式**

以下用作布尔表达式时均为 False：

```javascript
null
undefined
''  // 空字符串
0   // 数字0
```

但同时要注意，以下在布尔表达式中始终为True：

```javascript
'0' // 字符串'0'
[]  // 空数组
{}  // 空对象
```

基于以上结论，我们可以把下面的代码：

```javascript
if (x != null)
```

精简为：

```javascript
if (x)
```

同样，如果你想判断一个变量既不为null，也不是空字符串的话，不必用：

```javascript
if (x != null && x != '')
```

只需要：

```javascript
if (x)
```

即可。

注意，有一些很容易搞错的布尔表达式。以下列举出一部分：

```javascript
Boolean('0') == true
'0' != true
0 != null
0 == [] //特别注意，0 == false, [] == true, 但是 0 == []
0 == false
Boolean(null) == false // 这个也要特别注意
null != true
null != false
Boolean(undefined) == false
undefined != true
undefined != false
Boolean([]) == true
[] != true
[] == false
Boolean({}) == true
{} != true
{} != false
NaN != true
NaN != false
Boolean(NaN) == false
```

这里很容易混淆，最好自己多实践一下。能用 `if (x)` 来判断的，不一定能用 `if (x == true)` 来判断。 

**三目运算符**

对于下面这种简单的true返回a,false返回b的判断：

```javascript
if(condition) {
    return a;
} else {
    return b;
}
```

可以采用三目运算符简写为：

```javascript
return (condition) ? a : b;
```

在生成HTML时，这种表达方式尤其有用：

```javascript
var cls = isFocused ? 'class="chk-focus"' : '';
var checkbox = '<input type="checkbox" />'
```

**逻辑运算符**

由逻辑与（`&&`）和逻辑或（`||`）运算符连接的表达式会从左到右依次执行，直到遇到满足条件为止，因此逻辑或（`||`）运算符也可以当作默认值运算符来用。比如：

```javascript
function doSomething(jQuery) {
    var $;
    if (jQuery) {
        $ = jQuery;
    } else {
        $ = window.jQuery;
    }
    // other code
}
```

可以简写为：

```javascript
function doSomething(jQuery) {
    var $ = jQuery || window.jQuery;
}
```

逻辑与(&&)也可以做类似的使用（当满足左边条件时执行右边的语句）。比如

```javascript
if('function' == typeof pgvMain) {
    pgvMain();
}
```

可以简写为：

```javascript
'function' == typeof pgvMain && pgvMain();
```

**节点遍历操作**

我们经常有类似这样的操作：获取一组节点，然后对这个节点数组（节点列表）进行遍历。通常代码是这样的：

```javascript
var divs = document.getElementsByTagName('div');
for (var i = 0; i < divs.length; i++) {
  doSomething(divs[i]);
}
```

这样的操作，假如获取节点长度（divs.length）的复杂度是 O(n)，获取某个子节点的复杂度也是 O(n)，则由于每次要计算节点长度，因而遍历一遍所有节点，这个算法的时间复杂度就为 O(n^2)。用以下方法可降低时间复杂度：

```javascript
var divs = document.getElementsByTagName('div');
var size = divs.length;
for (var i = 0; i < size; i++) {
    doSomething(divs[i]);
}
```

这里先把节点长度存到一个局部变量中，以后每次循环不再计算节点长度，因此总的时间复杂度变为了 O(n) + 1; 还可以用另一种方法

```javascript
var divs = document.getElementsByTagName('div');
for (var i = 0, div; div = divs[i]; i++) {
    doSomething(div);
}
```

