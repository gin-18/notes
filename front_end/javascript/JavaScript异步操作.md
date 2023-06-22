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
setTimeout(
  function sayMyName(name) {
    console.log("my name is:", name);
  },
  3000,
  "xxx"
);

clearTimeout(timeoutId);

setInterval(
  function sayMyName(name) {
    console.log("my name is:", name);
  },
  3000,
  "xxx"
);

clearInterval(intervalId);
```

上面的代码，直接使用 `clearTimeout` 和 `clearInterval` 函数清除了定时器，所以定时器不会有任何输出。

## 参考链接

---

[https://wangdoc.com/javascript/async/general](https://wangdoc.com/javascript/async/general)

[https://wangdoc.com/javascript/async/timer](https://wangdoc.com/javascript/async/timer)
