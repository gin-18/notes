# ES6

[TOC]

---

## let 和 const

---

`let` 和 `const` 声明的变量有如下特点：

1. 不存在变量提升

2. 不允许重复声明

3. 具有块级作用域

4. 暂时性死区

5. 不与顶层对象挂钩

### 暂时性死区

只要块级作用域内存在 `let` 命令，则 `let` 命令声明的变量就 `绑定` 在这个区块内，不再受外部影响。

```javascript
let a = 1;

function f(){
  console.log(a)
  let a = 2;
}
f() // ReferenceError: Cannot access 'a' before initialization
```

`let` 声明的变量 `绑定` 在这个区块内，区块内的打印语句访问不到外部声明的变量 `a`。

## 变量的解构赋值

---

### 数组的解构赋值

---

基本用法:

```javascript
let [foo, [bar, baz]] = [1, [2, 3]];

foo // 1
bar // 2
baz // 3
```

### 对象的解构赋值

---

基本用法：

```javascript
let { foo, bar } = { foo: "aaa", bar: "bbb" };

foo // aaa
bar // bbb
```

## 模板字符串

---

模板字符串是增强版的字符串，用 `反引号` 标识。

模板字符串可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。

模板字符串中可以嵌入变量，需要将变量名写在 `${}` 之中。

```javascript
// 普通字符串
`this is a string`

// 多行字符串
`this
is
a
string
`

// 字符串内嵌变量
let name = "gin";
`my name is ${name}`
```

`${}` 的大括号中可以放任意的 JavaScript 表达式，可以进行运算，以及引用对象的属性。

```javascript
let a = 1;
let b = 2;

`${a} + ${b} = ${a + b}` // 1 + 2 = 3

// 对象属性的引用
let obj = {
  c: 3,
  d: 4,
}
`${obj.c + obj.d}` // 7
```

模板字符串中还可以调用函数。

```javascript
function f() {
  return "gin"
}

`my name is ${f()}` // my name is gin
```

## 函数的扩展

---

### 函数参数的默认值

---

ES6 允许为函数的参数设置默认值，即直接写在参数定义的后面。

```javascript
function f(a, b = 2) {
  return [a, b];
}

f(1) // [1, 2]
f(1, 5) // [1, 5]
```

### 参数默认值的位置

---

定义默认值的参数，应该是函数的尾参数。如果非尾部的参数设置了默认值，实际上这个参数是无法省略的。

```javascript
function f(a = 1, b) {
  return [a, b];
}

f() // [1, undefined]
f(2) // [2, undefined]
f(, 3) // 报错
f(undefined, 3) [1, 3]
f(2, 3) // [2, 3]
```

上面的代码中， 非尾参数 `a` 设置了默认值，这时，无法只省略该参数，除非显式的传入 `undefined`。

### rest 参数

---

`rest` 参数，形式为 `...变量名`，用于获取函数多余的参数，这样就不需要使用 `arguments` 对象了。

`rest` 参数中的 `变量` 是一个 `数组`，该 `变量` 将多余的参数放入 `数组`。

`rest` 参数之后不能再有其他参数。

```javascript
function f(...args) {
  return args;
}

f(1, 2, 3) // [1, 2, 3]

// 报错
function fn(a, ...args, b) {
  // ...
}
```

### 箭头函数

---

ES6 允许使用 `=>` 定义函数，其形式如下：

```javascript
let f = a => a;

// 等同于

let f = function (a) {
  return a;
}
```

如果箭头函数中没有参数或者有多个参数，就需要使用 `()` 代表参数部分。

```javascript
let f = () = 1;

// 等同于

let f = function () {
  return 1;
}

let fn = (a, b) => a + b;

// 等同于

let fn = function (a, b) {
  return a + b;
}
```

如果箭头函数的代码块部分多余一条语句，就需要使用 `{}` 将代码包裹起来，并使用 `return` 语句返回。

```javascript
let f = (a, b) => {
  let sum = a + b;
  return sum;
}
```

如果箭头函数需要直接返回一个对象，必须在对象的外面加上 `()`，不然代码会报错。

```javascript
// 报错
let f = (a, b) => {name: a, age: b}

// 不报错
let f = (a, b) => ({name: a, age: b})
```

使用箭头函数的注意点：

1. 箭头函数没有自己的 `this` 对象，箭头函数内部的 `this` 就是函数定义时上层作用域中的 `this`。

2. 不可以当作 `构造函数`。

3. 不可以使用 `arguments` 对象，可以使用 `rest` 参数代替。

4. 不可以使用 `yield` 命令，因此箭头函数不能用作 `Generator` 函数。

## 数组的扩展

---

### 扩展运算符

---

`...` 扩展运算符可以将一个数组转为用逗号分隔的参数序列。

```javascript
let array = [1, 2, 3];

console.log(...array); // 1 2 3
```

#### 扩展运算符的应用

---

##### 复制数组

---

数组是一个复合类型，直接复制只是复制了指向底层数据结构的指针，而不是克隆一个新数组。

```javascript
let array_01 = [1, 2, 3];

let array_02 = [...array_01]; // [1, 2, 3]
```

##### 合并数组

---

扩展运算符提供了合并数组的新写法。

```javascript
let array_01 = [1, 2, 3];
let array_02 = [4, 5, 6];

[...array_01, ...array_02]; // [1, 2, 3, 4, 5, 6]
```

##### 展开字符串

---

扩展运算符可以将字符串展开成真正的数组。

```javascript
[..."hello"]; // ["h", "e", "l", "l", "o"]
```

## 对象的扩展

---

### 属性的简洁表示

---

ES6 中允许在大括号中，直接写入 `变量` 和 `函数`，作为对象的属性和方法。

```javascript
// 属性的简写
let a = 1;
let obj = {a};

// 等同于

let obj = {
 a: a,
}

// 方法的简写
let obj_f = {
  method() {
    return "hello"
  }
}

// 等同于

let obj = {
  method() {
    return "hello";
  },
};
```

### 属性名表达式

---

用表达式作为属性名，需要将表达式放在 `[]` 内。

```javascript
let obj = {
  a: 1,
}

obj["b" + "c"] = 2
```

### 对象的扩展运算符

---

对象的扩展运算符是 `ES2018` 引入的。

对象的扩展运算符 `...` 用于取出参数对象的所有可遍历属性，拷贝到当前对象之中。

```javascript
let obj_01 = {
  a: 1,
  b: "hello",
}

let obj_02 = {...obj_01}
0bj_02 // { a: 1, b: "hello" }
```

## Symbol

---

`Symbol` 是一种新的数据类型，表示 `独一无二` 的值。

`Symbol` 值通过 `Symbol()` 函数生成。

`Symbol()` 函数前面不能使用 `new` 命令。

现在对象的属性名可以有两种类型：`字符串` 和 `Symbol`。

`Symbol()` 函数可以接受一个字符串作为参数，表示对 `Symbol` 实例的描述。

```javascript
let name = symbol("name")
let gender = symbol("gender")

let obj = {
  [name]: "gin",
  [gender]: "male",
}

obj.name = "leo"

obj // { name: "leo", [Symbol(name)]: "gin", [Symbol(gender)]: "male" }
```

上面的代码中，添加了新的属性 `name` 并不会与 `Symbol` 类型的属性名冲突。

## Set 数据结构

---

`Set` 类似于数组，但是成员的值都是唯一的，没有重复的值。

`Set` 本身是一个构造函数，用于生成 `Set` 数据结构。

```javascript
let set = new Set([1, 2, 3, 3, 4, 5, 6, 6])

[...set] // [1, 2, 3, 4, 5, 6]
```

### Set 实例属性

---

* `Set.prototype.constructor`：构造函数，默认是 `Set` 函数。

* `Set.prototype.size`：返回 `Set` 实例的成员总数。

### Set 实例的操作方法

---

`Set.prototype.add(value)`：添加某个值，返回 `Set` 结构本身。

`Set.prototype.delete(value)`：删除某个值，返回一个布尔值，表示是否删除成功。

`Set.prototype.has(value)`：返回一个布尔值，表示该值是否为 `Set` 结构的成员。

`Set.prototype.clear()`：清除所有成员，没有返回值。

### Set 实例的遍历方法

---

`Set.prototype.keys()`：返回键名的遍历器。

`Set.prototype.values()`：返回键值的遍历器。

`Set.prototype.entries()`：返回键值对的遍历器。

`Set.prototype.forEach()`：使用回调函数遍历每个成员。

### 使用 Set 结构实现去重操作

---

数组去重。

```javascript
let a = [1, 2, 2, 2, 3, 3, 4, 5, 5, 6]

[...new Set(a)] // [1, 2, 3, 4, 5, 6]
```

字符串去重。

```javascript
let s = "stringssttring"

[...new Set(s)].join("") // string
```

## async 函数和 await 命令

---

### async

---

`async` 函数返回一个 `Promise` 对象。

`async` 函数内部 `return` 语句返回的值，会成为 `then()` 方法回调函数的参数。

```javascript
async function f() {
  return "this is an async function";
}

t().then((res) => {
  console.log(res); // this is an async function
});
```

`async` 函数内部抛出异常，会导致返回的 `Promise` 对象变为 `rejected` 状态。抛出的错误对象会被 `catch()` 方法的回调函数接收。

```javascript
async function e() {
  throw new Error("this is an error message");
}

e().catch((err) => {
  console.log(err); // this is an error message
});
```

### 返回 `Promise` 对象的状态变化

---

`async` 函数返回的 `Promise` 对象，必须等到内部所有 `await` 命令后面的 `Promise` 对象执行完，才会发生状态改变，除非遇到 `return` 语句或抛出错误。也就是说，只有 `async` 函数内部的异步操作执行完成，才会执行 `then()` 方法指定的回调函数。

```javascript
function t_1(t) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("this is first");
    }, t);
  });
}

function t_2(t) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("this is second");
    }, t);
  });
}

async function aw() {
  let t1 = await t_1(1000);
  let t2 = await t_2(2000);
  return `${t1} + ${t2}`;
}

aw().then((res) => {
  console.log(res);
});
```

上面的代码中，只有 `t_1()` 函数和 `t_2()` 函数中的操作完成，才会执行 `then()` 方法里面的打印语句。

### await 命令

---

正常情况下，`await` 命令后面是一个 `Promise` 对象，返回该对象的结果。如果不是，直接返回对应的值。

```javascript
async function t() {
  return await "hello";
}

t().then((res) => {
  console.log(res);
});
```

`await` 命令后面的 `Promise` 对象的状态变为 `rejected`，则 `reject` 的参数会被 `catch()` 方法的回调函数接收。

任何一个 `await` 语句后面的 `Promise` 对象变为 `rejected` 状态，那么整个 `async` 函数都会中断执行。

```javascript
async function t() {
  await Promise.reject("error");
  await Promise.resolve("success");
}

t()
  .then((res) => {
    console.log(res);
  })
  .catch((e) => {
    console.log(e);
  });
```

上面的代码中，第二个 `await` 语句不会执行，因为第一个 `await` 语句状态变成了 `rejected`。

如果，需要在前一个异步操作失败，也不中断后面的异步操作。这时，可以将第一个 `await` 放在 `try...catch` 结构中，这样不管第一个异步操作是否成功，第二个 `await` 都会执行。

```javascript
async function t() {
  try {
    await Promise.reject("error");
  } catch (error) { }
  return await Promise.resolve("success");
}

t()
  .then((res) => {
    console.log(res);
  })
```

### 使用注意点

---

1. `await` 命令后面的 `Promise` 对象运行结构可能是 `rejected`，所以最好把 `await` 命令放在 `try...catch` 中。

```javascript
async function t() {
  try {
    await fetch();
  } catch (error) {
    console.log(error);
  }
}

// 另一种写法
async function t() {
  await fetch().catch((error) => {
    console.log(error);
  });
}
```

2. 如果多个 `await` 命令后面的异步操作不存在继发关系，最好让它们同时触发。

```javascript
async function aw() {
  let t1 = await t_1(1000);
  let t2 = await t_2(2000);
}
```

上面的代码中，`t_1()` 函数和 `t_2()` 函数是两个独立的异步操作，被写成继发关系，这样会比较耗时，因为只有 `t_1()` 函数完成后，才会执行 `t_2()` 的操作。此时，可以让它们同时触发。

```javascript
let [t1, t2] = await Promise.all([t_1(), t_2()])
```

上面的代码中， `t_1()` 函数 和 `t_2()` 函数同时触发，可以缩短执行时间。























