# JavaScript 异步操作

---

[TOC]

## 单线程模式

---

`单线程模式` 指的是同时只能执行一个任务，其他任务必须在后面排队。

JavaScript 采用的就是 `单线程模式`。

## 同步任务和异步任务

---

`同步任务` 是那些没有被引擎挂起，在 `主线程` 上排队执行的任务，只有前一个任务执行完成，后一个任务才能执行。

`异步任务` 是那些被引擎挂起，`不进入主线程`，而进入 `任务队列` 的任务。只有引擎认为某个异步任务可以执行了，该任务才会进入主线程执行。排在异步任务后的代码，不用等到异步任务执行结束，而是马上执行。

## 任务队列和事件循环

---

JavaScript 运行时，引擎提供一个 `任务队列`，里面是各种当前程序需要处理的 `异步任务`。

JavaScript 在运行时，会不停地检查，只要同步任务执行完成，引擎就会去检查被挂起的异步任务，是否可以进入主线程。这种循环检查的机制，就是 `事件循环`。

首先，主线程会执行所有的同步任务。等到同步任务执行完成，就会去看任务队列里面的异步任务。满足条件的异步任务重新进入主线程开始执行，这时这个异步任务就变成了同步任务。等到执行完成，下一个异步任务再进入主线程开始执行。一旦任务队列清空，程序就结束。

## 定时器

---

### setTimeout()

---

`setTimeout` 函数用来指定 `某个函数` 或 `某段代码`，在 `多少毫秒` 之后执行，并返回一个 `整数`，表示 `定时器的编号`，这可以用来取消这个定时器。

```javascript
setTimeout(() => {
  console.log("1");
}, 3000);
```

`setTimeout` 函数的 `第一个参数` 是所要执行的 `函数` 或 `代码`；`第二个参数` 是等待的毫秒数。

`setTimeout` 函数还允许更多参数，这些参数会作为第一个参数的是函数的参数传入。

```javascript
setTimeout(
  function sayMyName(name) {
    console.log("my name is:", name);
  },
  3000,
  "xxx"
);
```

上面的代码，`setTimeout` 的 参数 `xxx` 作为 `sayMyName` 函数的参数传入。

### setInterval()

---

`setInterval` 函数的用法和 `setTimeout` 函数完全一致，区别是 `setInterval` 函数指定某个任务每隔一段时间就会执行一次，也就是无限次的定时执行。

```javascript
setInterval(function sayMyName(name) {
  console.log("my name is:", name);
}, 3000, "xxx");
```

上面的代码，每隔 `3000` 毫秒，就会执行一次 `sayMyName` 函数。

### clearTimeout() 和 clearInterval()

---

`setTimeout` 和 `setInterval` 函数，都返回一个整数值，表示定时器编号。将该整数传入 `clearTimeout` 和 `clearInterval` 函数，就可以取消对应的定时器。

```javascript
var timeoutId = setTimeout(
  function sayMyName(name) {
    console.log("my name is:", name);
  },
  3000,
  "xxx"
);

clearTimeout(timeoutId);

var intervalId = setInterval(
  function sayMyName(name) {
    console.log("my name is:", name);
  },
  3000,
  "xxx"
);

clearInterval(intervalId);
```

上面的代码，直接使用 `clearTimeout` 和 `clearInterval` 函数清除了定时器，所以定时器不会有任何输出。

## Promise 对象

---

`Promise` 对象代表一个异步操作，有 `3` 种状态：`pending(进行中)`、`fulfilled(已成功)` 和 `rejected(已失败)`。只有异步操作的结果可以决定当前是哪一种状态，任何操作都无法改变这个状态。

`Promise` 对象的状态改变只有 `2` 种可能：

1. 从 `pending` 变为 `fulfilled`。

2. 从 `pending` 变为 `rejected`。

只要这两种情况发生，状态就凝固了，会一直保持这个结果，这时就称为 `resolved(已定型)`。

### 基本用法

---

`Promise` 对象是一个构造函数，用来生成实例对象。

```javascript
var promise = new Promise((resolve, reject) => {
  if(/* 异步成功 */) {
    resolve(value)
  } else {
    reject(error)
  }
})
```

`Promise` 构造函数接受一个函数作为参数，这个函数有 `2` 个参数分别是：`resolve` 和 `reject`。这两个参数都是函数，由 JavaScript 引擎提供。

* `resolve()` 函数的作用是将 `Promise` 对象的状态从 `pending` 变为 `resolved`。在异步操作成功时调用，并将异步操作的结果作为 `resolve()` 函数的参数传递出去。

* `reject()` 函数的作用是将 `Promise` 对象的状态从 `pending` 变为 `rejected`。在异步操作失败时调用，并将异步操作报出的错误作为 `reject()` 函数的参数传递出去。

简单用 `Promise` 对象封装一个读取文件内容的函数。

```javascript
const fs = require("fs");

function rf(filePath) {
  return new Promise((resolve, reject) => {
    fs.readFile(filePath, (error, data) => {
      if (error) return reject(error);
      resolve(data);
    });
  });
}
```

### Promise.prototype.then()

---

`then()` 方法为 `Promise` 实例添加状态改变时的回调函数。

`then()` 方法的第一个参数是 `resolved` 状态的回调函数，第二个参数是 `rejected` 状态的回调函数，这两个参数都是可选的。

`then()` 方法返回一个新的 `Promise` 实例，因此可以链式调用。

```javascript
rf("/post.json")
  .then(res => res)
  .then(res => {
    console.log(res);
  });
```

### Promise.prototype.catch()

---

`catch()` 方法用于指定发生错误时的回调。

```javascript
rf("/post.json")
  .then(res => res)
  .catch(error => {
    console.log(error);
  });
```

`Promise` 对象的错误具有 `冒泡` 性质，会一直向后传递，直到被捕获为止。也就是说，错误总会被下一个 `catch` 语句捕获。

一般来说，不要在 `then()` 方法里面定义 `rejected` 状态的回调函数，总是使用 `catch()` 方法。

```javascript
// 不好的写法
rf("/post.json".then(
  (res) => res,
  (e) => {
    console.log(e);
  });

// 更好的写法
rf("/post.json")
  .then((res) => res)
  .catch((e) => {
    console.log(e);
  });
```

### Promise.all()

---

`Promise.all()` 方法用于将多个 `Promise` 实例包装成一个新的 `Promise` 实例。

`Promise.all()` 方法接受一个 `数组` 作为参数。

```javascript
let p = Promise.all([p1, p2, p3]) // p1, p2, p3 都是 Promise 实例
```

上面的代码中，`p` 的状态由 `p1`、`p2` 和 `p3` 决定，分为以下 `2` 种情况：

1. 只有 `p1`、`p2` 和 `p3` 的状态都变成 `fulfilled`，`p` 的状态才会变成 `fulfilled`。此时 `p1`、`p2` 和 `p3` 的返回值组成一个数组传递给 `p` 的回调函数。

2. 只要 `p1`、`p2` 和 `p3` 之中有一个状态是 `rejected`，`p` 的状态就变成 `rejected`。此时第一个 `rejected` 的实例的返回值就会传递给 `p` 的回调函数。

## 参考链接

---

* [https://wangdoc.com/javascript/async/general](https://wangdoc.com/javascript/async/general)

* [https://wangdoc.com/javascript/async/timer](https://wangdoc.com/javascript/async/timer)

* [https://wangdoc.com/es6/promise](https://wangdoc.com/es6/promise)
