# JavaScript 数据类型

---

[TOC]

## 概述

---

JavaScript 的数据类型共有 `6种`：

* 数值(number)：整数和小数。

* 字符串(string)：文本。

* 布尔值(boolean)：表示真伪的两个特殊值。

* undefined：表示未定义或不存在。

* null：表示空值。

* 对象：各种值的集合。

通常，数值、字符串、布尔值这三种类型，是最基本的数据类型，称为 `原始类型` 的值。

对象往往是多个原始类型的值合成，所以，对象称为 `合成类型` 的值。

`undefined` 和 `null`，一般看成两个特殊值。

对象是复杂的数据类型，又可以分为三个子类型：

* 狭义的对象(object)

* 数组(array)

* 函数(function)

## typeof 运算符

---

`typeof` 运算符可以返回一个值的数据类型。

数值、字符串、布尔值分别返回 `number`、`string`、`boolean`。

```javascript
typeof 1 // "number"

typeof "hello" // "string"

typeof true // "boolean"
```

函数返回 `function`。

```javascript
function f() {}

typeof f // "function"
```

undefined 返回 `undefined`。

```javascript
typeof undefined // undefined
```

对象返回 `object`。

`空数组` 返回的也是 `object`。

```javascript
typeof {} // "object"

typeof [] // "object"
```

`null` 返回的是 `object`。

```javascript
typeof null // "object"
```

`null` 的类型是 `object`，是由于历史原因造成的。1995年的 JavaScript 语言的第一版，只设计了 `五种` 数据类型(`对象`、`整数`、`浮点数`、`字符串`和`布尔值`)，没有考虑 `null`，只把 `null` 当作 `object` 的一种特殊值。后来 `null` 独立出来，作为一种单独的数据类型。为了兼容以前的代码，`typeof null` 返回 `object` 就没法改变了。

## null 和 undefined

---

`null` 和 `undefined` 都表示“没有”。

`null` 转为数值时为 `0`；`undefined` 转为数值时为 `NaN`。

```javascript
Number(null) // 0

Number(undefined) // NaN
```

## 布尔值

---

布尔值只有 `true` 和 `false` 这两个值。

如果 JavaScript 预期某个位置应该是布尔值，会将该位置上现有的值自动转换为布尔值。

转换规则是除了以下 `6` 个值被转为 `false`，其他都转为 `true`。

* undefined

* null

* false

* 0

* NaN

* 空字符串

`空对象` 和 `空数组` 对应的布尔值都是 `true`。

```javascript
if ({}) {
  console.log(true);
}
// true

if ([]) {
  console.log(true);
}
// true
```

## 数值

---

### 整数和浮点数

---

JavaScript 底层没有整数，所有数字都是 `64位浮点数`。

由于浮点数不是精确的数，所以涉及小数的比较和运算都要小心。

```javascript
0.1 + 0.2 === 0.3 // false
```

### 数值的进制

---

JavaScript 对整数提供 `4种` 进制的表示方法。

* 十进制：没有前导0的数值。

* 八进制：有前缀 `0o` 或 `00` 的数值。

* 十六进制：有前缀 `0x` 或 `0X` 的数值。

* 二进制：有前缀 `0b` 或 `0B` 的数值。

```javascript
0x10 // 16
0o10 // 8
0b10 // 2
```

### 特殊数值

---

#### NaN

---

`NaN` 表示 `非数值`，主要出现在将字符串解析为数字出错的场景。

```javascript
1 - "a" // NaN
```

上面的代码，会自动将字符串 `a` 转为数值，但由于 `a` 不是数值，所以最后的结果为 `NaN`，表示 `非数值`。

#### Infinity

---

`Infinity` 表示 `无穷`，用来表示 `正的数值太大` 或 `负的数值太小`。

`Infinity` 有正负之分，`Infinity` 表示正无穷，`-Infinity` 表示负无穷。

```javascript
Infinity === -Infinity // false
```

### 数值相关的全局方法

---

#### parseInt 方法

---

`parseInt` 方法用于将 `字符串` 转为 `整数`。

```javascript
parseInt("123") // 123
```

字符串转为整数时，是一个个字符依次转换的。如果遇到不能转为数字的字符，就不再进行下去，返回已经转好的部分。

```javascript
parseInt("16a") // 16
```

`parseInt` 方法还可以接受第二个参数(2-36之间)，表示被解析的值的进制，返回该值对应的十进制数，第二个参数的默认值为 `10`。

```javascript
parseInt("10") // 10

parseInt("10", 2) // 2

parseInt("10", 8) // 8

parseInt("10", 16) // 16
```

#### parseFloat 方法

---

`parseFloat` 方法用于将一个 `字符串` 转为 `浮点数`。

```javascript
parseFloat("3.14") // 3.14
```

如果字符串符合科学计数法，则会进行相应的转换。

```javascript
parseFloat("3.14e+2") // 314
```

如果字符串的第一个字符不能转为浮点数，则返回 `NaN`。

```javascript
parseFloat("xxx") // NaN
```

#### isNaN 方法

---

`isNaN` 方法可以判断一个值是否为 `NaN`。

```javascript
isNaN("xxx") // true

isNaN(124) // false
```

不过，对于 `空数组` 和 `只有一个数值元素的数组`，`isNaN` 方法返回 `false`。

```javascript
isNaN([]) // false

isNaN([123]) // false
```

## 字符串

---

如果 `长字符串` 必须分成多行，可以在每行的末尾使用 `反斜杠`。

```javascript
var longString = "long \
string"

// long string
```
### 转义

---

`反斜杠` 用来表示一些特殊字符，又称为 `转义符`。

需要转义的特殊字符有下面这些：

* `\0`：null

* `\b`：后退键

* `\f`：换页符

* `\n`：换行符

* `\r`：回车符

* `\t`：制表符

* `\v`：垂直制表符

* `\'`：单引号

* `\"`：双引号

* `\\`：反斜杠

### 字符串与数组

---

字符串可以被视为字符数组，可以 `下标` 访问字符串某个位置的字符。

```javascript
var s = "hello";

s[0] // h
```

### length 属性

---

`length` 属性返回字符串的长度，该属性是无法改变的。

```javascript
var s = "hello"

s.length // 5

s.length = 3
s.length // 5
```

### 字符集

---

JavaScript 使用 `Unicode` 字符集，所有字符都用 `Unicode` 表示。

JavaScript 允许直接使用 `Unicode` 码点表示字符串，即将字符串写成 `\uxxxx` 的形式。

每个字符在 JavaScript 内部都是以 `16位(2个字节)` 的 `UTF-16` 格式储存。因此，JavaScript 的单位字符长度固定为 `16位` 长度，即 `2个字节`。所以，对于码点在 `U+10000` 到 `U+10FFFF` 之间的字符，JavaScript 总是认为是两个字符。

## 对象

---

`对象` 就是一组 `键值对` 的集合。

```javascript
var obj = {
  name = "xxx",
  age = 18
}
```

上面的代码，使用 `{}` 定义了一个对象并赋值给 `变量obj`。第一个键值对是 `name: "xxx"`，键名是 `name`，键值是 `xxx`。对象中，键值对之间使用 `,` 分隔。

对象中，每个键名又称为 `属性`，如果，其中的属性值为 `函数`，则把这个属性称为 `方法`。

```javascript
var obj = {
  f: function(a) {
    return a
  }
}

obj.f(16) // 16
```

### 属性的操作

---

#### 属性的读取

---

读取属性有两种方法：

* 点运算符 `.`

* 方括号运算符 `[""]`

```javascript
var obj = {
  name: "xxx"
}

obj.name // xxx
obj["name"] // xxx
```

#### 属性的赋值

---

`点运算符` 和 `方括号运算符` 不仅可以读取属性，还可以对属性进行赋值。

```javascript
var obj = {
  name: "xxx"
}

obj.name = "sss" // sss
obj["name"] = "sss" // sss
```

JavaScript 允许属性的 `后绑定`，即可以随时新增属性。

```javascript
var obj = {
    name: "xxx"
}

等价于

obj = {}
obj.name = "xxx"
```

#### 属性的查看

---

查看一个对象本身的所有属性，可以使用 `Object.keys` 方法。

```javascript
var obj = {
  name: "xxx",
  age: 18
}

Object.keys(obj); // ["name", "age"]
```

#### 属性的删除

---

`delete` 命令可以删除对象的属性，删除成功后返回 `true`。

```javascript
var obj = {
  name: "xxx"
}

delete obj.name;

Object.keys(obj); // []
```

#### in 运算符

---

`in` 运算符用于检查对象是否包含某个属性。如果包含返回 `true`，否则返回 `false`。

```javascript
var obj = {
  name: "xxx"
}

"name" in obj // true

"toString" in obj // true
```

`in` 运算符不能识别哪些属性是对象自身的，哪些属性是继承的，所以上面的代码，`toString` 也返回了 `true`。

这时，可以使用对象的 `hasOwnProperty` 方法判断一个属性是否为对象自身的属性。

```javascript
var obj = {
  name: "xxx"
}

obj.hasOwnProperty("name") // true

obj.hasOwnProperty("toString") // false
```

#### for...in 属性的遍历

---

`for...in` 循环用来遍历一个对象的全部属性。

```javascript
var obj = {
  name: "xxx",
  age: 18
}

for (var i in obj) {
  console.log("key", i);
  console.log("value", obj[i]);
}

// key name
// value xxx

// key age
// value 18
```

`for...in` 遍历时，会跳过不能遍历的属性，遍历对象所有可以遍历的属性。

`for...in` 不仅可以遍历自身的属性，还可以遍历继承属性。

## 函数

---

### 函数的声明

---

#### function 命令

---

```javascript
function 函数名(参数) {
  函数体
}
```

#### 函数表达式

---

除了使用 `function` 命令声明函数，还可以使用变量赋值的写法。

```javascript
var 函数名 = function(参数) {
  函数体
}
```

上面的代码，将一个 `匿名函数` 赋值给一个变量，`匿名函数` 又称为 `函数表达式`。因为赋值语句 `=` 的右边只能放表达式。

### 返回值

---

函数体内部的 `return` 语句，表示返回。

`return` 语句后接一个表达式，这个 `表达式的值` 就是 `函数的返回值`。

函数体执行到 `return` 语句就会停止执行，`return` 语句后面的代码就不会执行了。

```javascript
function sum(a, b) {
  return a + b;
  console.log("打印语句不会执行了");
}

sum(1, 2) // 3
```

上面的代码，函数的返回值就是 `参数a` + `参数b ` 的值。并且 `console.log` 语句不会执行。

### 函数名提升

---

JavaScript 会将 `函数名` 看作 `变量名`。所以，采用 `function` 命令声明函数时，`整个函数` 会提升到代码的头部。

```javascript
sum(1, 2); // 3

function sum(a, b) {
  return a + b;
}
```

上面的代码，虽然在函数声明前就调用了函数 `sum`，但是，由于函数名提升，所以，在函数调用之前，函数就已经声明了。

不过，使用 `函数表达式` 声明的函数，并不是 `整个函数` 提升到代码的头部。

```javascript
sum(1, 2) // TypeError: undefined is not a function

var sum = function(a, b) {
  return a + b;
}
```

上面的代码，等同于下面的代码：

```javascript
var sum;

sum(1, 2); // TypeError: undefined is not a function

sum = function(a, b) {
  return a + b;
}
```

使用 `函数表达式` 声明的函数，只是 `变量` 提升到代码头部。

### 函数的属性和方法

---

#### name 属性

---

`name` 属性返回函数的名字。

```javascript
function sum(a, b) {
  return a + b;
}

sum.name // sum
```

#### length 属性

---

`length` 属性返回 `形参` 个数。

```javascript
function sum(a, b) {
  return a + b;
}

sum.length // 2
```

#### toString 方法

---

函数的 `toString` 方法返回一个字符串，内容是函数的源码。

```javascript
function sum(a, b) {
  return a + b;
}

sum.toString()
// function sum(a, b) {
//   return a + b;
// }
```

### 函数作用域

---

作用域是指变量存在的范围，在 `ES5` 中只有 `2种` 作用域：

* 全局作用域：整个程序一直存在，所有地方都可以读取

* 函数作用域：变量只在函数内部存在

```javascript
var a = 1;

function f() {
  console.log(a)
}

f() // 1
```

上面的代码，在函数内部可以访问全局变量。

然而，在函数内部定义的变量，函数外部是无法读取的，称为 `局部变量`。

```javascript
function f() {
  var a = 1;
}

console.log(a) // ReferenceError: a is not defined
```

注意：用 `var` 命令声明的变量，只有在函数内部声明的才是局部变量，在其他区块内，一律都是全局变量。

```javascript
for (var i = 0; i < 2; i++) {
  console.log(i) // 1, 2
}

console.log(i) // 2
```

上面的代码，在 `for` 循环中定义的 `变量i` 在循环外也是可以访问的。

### 函数内部的变量提升

---

在函数作用域中，使用 `var` 命令声明的变量，不管在什么位置，都会提升到函数的头部。

```javascript
function f() {
  for (var i = 0; i < 2; i++) {
    console.log(i) // 1, 2
  }
}

等同于

function f() {
  var i;
  for (i = 0; i < 2; i++) {
    console.log(i) // 1, 2
  }
}
```

### 函数本身的作用域

---

函数本身的作用域就是 `函数声明时所在的作用域`，与其运行所在的作用域无关。

```javascript
var a = 1;

function f() {
  console.log(a)
}

function e() {
  var a = 2;
  f()
}

e() // 1
```

上面的代码，`函数f` 是在 `函数e` 外部声明的，所以 `函数f本身的作用域` 是绑定在外层的。所以，在 `函数f` 内访问 `变量a` 是在外部取的值，而不是在 `函数e` 内部取的值。

所以，函数执行时所在的作用域，是定义时的作用域，而不是调用时所在的作用域。

### 参数

---

#### 参数的传递方式

---

如果函数的参数是 `原始类型(数值、字符串、布尔值)` 的值，传递方式就是 `传值传递`，所以，在函数内部修改参数值，不会影响函数外部。

```javascript
var a = 1;

function f(a) {
  a = 2;
}

console.log(a) // 1
```

上面的代码，`变量a` 是一个原始类型的值，在函数内部，`a` 的值是原始值的拷贝，所以，无论怎么修改都不会影响原始值。

如果，参数是 `复合类型(数组、对象、函数)` 传递方式就是 `传址传递`，传入函数的是 `原始值的地址`。因此，在函数内修改参数，会影响到原始值。

```javascript
var arr = [1, 2];

function f(arr) {
  arr[0] = 3;
}

f(arr);

console.log(arr); // [3, 2]
```

上面的代码，传入 `函数f` 的是 `数组的地址`。因此，在函数内部修改 `数组arr` 的元素，会影响到原始值。

注意：如果在函数内部修改的不是 `参数中的某个值`，而是 `替换到整个参数`，则不会影响到原始值。

```javascript
var arr = [1, 2];

function f(arr) {
  arr = [3, 4];
}

f(arr);

console.log(arr); // [1, 2]
```

上面的代码，在函数中将参数数组替换成了另一个数组，这时不会影响到原始值。这是因为，在函数内部重新赋值，使得参数指向了另一个地址，所以，保存在原始地址的值不受影响。

#### arguments 对象

---

`arguments` 对象包含 `函数运行时的所有参数`，并且只能在 `函数体` 内使用。

`arguments` 对象和 `数组` 类似，可以使用 `下标` 访问 `arguments` 对象中的元素，例如，`arguments[0]` 就是第一个参数。`arguments` 对象的 `length` 属性表示函数调用时 `传入的参数个数`。 但是，数组的专有方法不能在 `arguments` 对象上直接使用。

```javascript
function f() {
  console.log(arguments[0]); // 1
  console.log(arguments[1]); // 2
  console.log(arguments.length); // 5
}

f(1, 2, 3, 4, 5);
```

`arguments` 对象还有一个 `callee` 属性，返回对应的原函数。

```javascript
function f() {
  console.log(arguments.callee === f); // true
}

f();
```

上面的代码，`arguments.callee` 和 `函数f` 本身是全等的。

### 立即调用的函数表达式(IIFE)

---

JavaScript 规定，如果 `function` 关键字出现在行首，一律解析成语句，所以，函数定义后立即调用的解决方法，就是不让 `function` 出现在行首，最简单的处理就是将其放在一个 `()` 内。

```javascript
(function() {
  ...
}());

或者

(function() {
  ...
})();
```

上面的代码，两种写法都是以 `()` 开头，JavaScript 引擎会认为这是一个表达式，而不是函数定义语句，这就叫 `立即调用的函数表达式`。

通常情况下，只对 `匿名函数` 使用 `立即调用的函数表达式`。其目的是：

* 不必为函数命名，避免污染全局变量

* `立即调用的函数表达式` 内部形成一个独立的作用域，可以封装一些外部无法读取的私有变量

## 数组

---

数组是按次序排列的一组值。每个值的位置都有编号(从0开始)，整个数组用方括号表示。

```javascript
var arr = [1, 2, 3];
```

上面的代码，定义了一个数组，`1` 是数组的 `0号位置`，`2` 是 `1号位置`，`3` 是 `3号位置`。

`任何类型` 的数据都可以放入数组中。

```javascript
var arr = [[1, 2], { name: "xxx"}, function f() { console.log("this is a function")}]

arr[0]; // [1, 2]
arr[1]; // { name: "xxx" }
arr[2]; // function f() { console.log("this is a function")}
```

### 数组的本质

---

数组的本质是一种特殊的对象。`typeof` 运算符返回的数组类型是 `object`。

```javascript
var arr = [1, 2, 3];

Object.keys(arr); // [0, 1, 2]
```

上面的代码，使用 `Object.keys` 方法返回数组的键名是 `[0, 1, 2]`。

### length 属性

---

数组的 `length` 属性返回 `数组成员的数量`。

```javascript
var arr = [1, 2, 3]

arr.length // 3
```

只要是数组就一定有 `length` 属性，该属性是一个动态的值。

```javascript
var arr = [1, 2];
arr.length // 2

arr[2] = 3;
arr.length // 3

arr[9] = 10;
arr.length // 10
```

上面的代码表明，数组的数字键不需要连续，`length` 属性的值总是比最大的那个整数键大 `1`。

### 数组的空位

---

当数组的某个位置是空元素，则称为 `数组存在空位`。

使用 `delete` 命令删除一个数组元素，会形成空位，但这不影响 `length` 属性。

```javascript
var arr = [1, 2, 3];

delete arr[0];

arr[0] // undefined
arr.length // 3
```

上面的代码，使用 `delete` 删除了 `arr` 数组的 `第0位`，但数组的 `length` 属性还是 `3`。

## 参考链接

---

* [https://wangdoc.com/javascript/types/general](https://wangdoc.com/javascript/types/general)

* [https://wangdoc.com/javascript/types/null-undefined-boolean](https://wangdoc.com/javascript/types/null-undefined-boolean)

* [https://wangdoc.com/javascript/types/number](https://wangdoc.com/javascript/types/number)

* [https://wangdoc.com/javascript/types/string](https://wangdoc.com/javascript/types/string)

* [https://wangdoc.com/javascript/types/object](https://wangdoc.com/javascript/types/object)

* [https://wangdoc.com/javascript/types/function](https://wangdoc.com/javascript/types/function)

* [https://wangdoc.com/javascript/types/array](https://wangdoc.com/javascript/types/array)
