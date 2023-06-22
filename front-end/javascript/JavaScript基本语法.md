[TOC]

## 变量

---

### 概念

---

变量是对 `值` 的引用，引用一个变量就相当于引用一个值。

在 JavaScript 中使用 `var` 关键字声明一个变量。

```javascript
var a = 1;
```

上面的代码声明了一个 `变量a` 并赋值 `1`。以后引用 `变量a` 就会得到值 `1`。

注：JavaScript 的变量名是区分大小写的，`A` 和 `a` 是两个不同的变量。

如果只声明了变量但是未赋值，则变量的值为 `undefined`, `undefined` 是一个特殊的值，表示 `未定义`。

```javascript
var a;

a // undefined
```

如果一个变量没有声明就直接使用，JavaScript 就会报 `变量未定义` 的错误。

```javascript
a // ReferenceError: x is not defined
```

JavaScript 是一种 `动态类型语言`, 变量的类型没有限制，可以随时改变。

```javascript
var a = 1;

a = "hello";
```

上面的代码先给 `变量a` 赋值为 `数值` 类型，第二次则重新赋值为 `字符串` 类型。

### 变量提升

---

JavaScript 引擎的工作方式是：先解析代码，获取所有的变量声明，再逐行运行。

这就造成了 `所有的声明语句会提升到代码的头部`，这就叫做 `变量提升`。

```javascript
console.log(a);

var a = "hello";
```

上面的代码先打印了 `变量a` 再声明变量，这不会报错，不过打印 `变量a` 的值为 `undefined`。

上面的代码相当于：

```javascript
var a;

console.log(a);

a = 1;
```

变量的声明 `var a` 提升到了代码的头部，所有打印语句结果为 `undefined`。

## 注释

---

注释的作用是对代码进行解释。

JavaScript 提供两种注释方式：

```javascript
// 单行注释

/*
  多
  行
  注
  释
*/
```

## 区块

---

JavaScript 使用大括号，将多个相关语句组合在一起，称为 `区块`。

使用 `var` 关键字声明的变量在区块内不构成单独的作用域。

```javascript
{
  var a = 1;
}

a // 1
```

上面的代码在一个区块内使用 `var` 关键字声明了 `变量a`，但是在区块外仍然能访问 `变量a`。

## 条件语句

---

### if 结构

---

`if` 语句先判断一个表达式的布尔值，根据布尔值的真伪，执行不同的语句。

```javascript
if (布尔值) {
  语句
  ...
}
```

上面的代码，只有 `布尔值为真` 时，才会执行区块内的语句。

### if...else 结构

---

`if` 语句后面还可以跟一个 `else` 代码块，表示条件不满足时，执行的代码。

```javascript
if (布尔值) {
  条件满足时，执行的语句
  ...
} else {
  条件不满足时，执行的语句
  ...
}
```

对同一个变量进行多次判断时，多个`if...else` 语句可以连在一起写。

```javascript
if (a === 0) {
  ...
} else if (a === 1) {
  ...
} else if (a === 2) {
  ...
} else {
  ...
}
```

### switch 结构

---

一个变量需要进行多次判断时，也可以使用 `switch` 语句。

```javascript
switch (a) {
  case "apple":
    ...
    break;
  case "banana":
    ...
    break;
  default:
    ...
}
```

`switch` 语句中比较运算的结果，采用的是 `===`, 而不是 `==`，这意味着比较时不会发生类型转换。

### 三元运算符

---

JavaScript 提供 `三元运算符` 也可以用于逻辑判断。

```javascript
(条件) ? 表达式1 : 表达式2;
```

上面代码中，如果 `条件` 判断为 `true`，则返回 `表达式1`的值，否则返回 `表达式2` 的值。

```javascript
var even = (a % 2 === 0) ? true : false;
```

上面代码中，如果 `变量a` 可以被 `2` 整除，则 `变量even` 的值为 `true`，否则为 `false`。

## 循环语句

---

### while 循环

---

`while` 语句包括一个 `循环条件` 和一段 `代码块`，只要 `循环条件` 为真，就不断循环执行代码块。

`while` 语句会先判断循环条件，再执行语句。

```javascript
while (条件) {
  语句
  ...
}
```

### do...while 循环

---

`do...while` 循环和 `while` 循环类似。

`do...while` 循环会先执行一次语句再判断循环条件。

```javascript
do {
  语句
  ...
} while (条件);
```

### for 循环

---

`for` 循环可以指定循环的 `起点`、`终点` 和 `终止条件`。

```javascript
for (初始表达式; 条件; 递增表达式) {
  语句
  ...
}
```

* 初始表达式：循环变量的初始值，只在循环开始时执行一次。

* 条件表达式：条件表达式为真时，才会继续执行循环。

* 递增表达式：每轮循环最后执行，用来递增循环变量。

```javascript
for (var i = 0; i < 2; i++) {
  console.log(i)
}

// 0
// 1
```

### break 语句和 continue 语句

---

`break` 语句和 `continue` 语句都具有跳转作用。

#### break 语句

---

`break` 语句用于跳出代码块或循环。

```javascript
for (var i = 0; i < 5; i++) {
  if (i === 1) break;
  console.log(i);
}

// 0
```

上面的代码，当循环执行到 `i === 1` 时，就会终止 `整个循环`，所以结果只会打印 `0`。

#### continue 语句

---

`continue` 语句用于立即 `终止本次循环`，返回循环的头部，开始下一轮循环。

```javascript
for (var i = 0; i < 5; i++) {
  if (i === 1) continue;
  console.log(i);
}

// 0
// 2
// 3
// 4
```

上面的代码，当代码执行到 `i === 1` 时，就会终止此次循环，所以不会打印 `1`，最终的结果是 `0、2、3、4`。

### 标签(label)

---

JavaScript 允许语句前面有标签，相当于定位符，用于跳转到程序的任意位置。

```javascript
label:
  语句
  ...
```

标签可以是任意字符，语句部分可以是任意语句。

标签通常和 `break` 语句和 `continue` 语句使用。

```javascript
top:
  // 打印九九乘法表
  for(var i = 1; i <= 9; i++) {
    for (var j = 1; j <= i; j++) {
      if (i === 2 && j === 2) break top;
      console.log(`${j} x ${i} = ${i * j}`);
    }
  }
```

上面的代码，当 `i === 2` 并且 `j === 2` 时，会跳出双重循环。

## 参考链接

---

[https://wangdoc.com/javascript/basic/grammar](https://wangdoc.com/javascript/basic/grammar)
