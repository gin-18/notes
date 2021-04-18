# Promise

`Promise`是一个构造函数，通过`new`关键字实例化对象。

`Promise`接受一个函数作为参数。

参数函数接受两个形参：`resolve`, `reject`。

```javascript
var promise = new Promise((resolve, reject)=>{})
```

## Promise实例的属性

`Promise`实例有2个重要的属性：state(状态)，result(结果)

## Promise的状态

第一种状态：pending(准备，待解决，进行中)

第二种状态：fulfilled(已完成，成功)

第三种状态：rejected(已拒绝，失败)

### Promise状态的改变

通过调用resolve()和reject()改变当前`Promise`对象的状态。

```javascript
var promise = new Promise((resolve, reject) => {
  resolve();
});
console.log(promise);
```

调用resolve()函数promise的状态会变为fulfilled。

```javascript
var promise = new Promise((resolve, reject) => {
  reject();
});
console.log(promise);
```

调用reject()函数promise的状态会变为rejected。

promise的状态只能改变一次。

### promise的结果

通过给resolve()函数和reject()函数传递参数可以改变当面promise对象的结果。

```javascript
var promise = new Promise((resolve, reject) => {
  resolve("succeed");
});
console.log(promise);
```

给resolve()函数传递参数改变的是promise对象fulfilled的结果。

```javascript
var promise = new Promise((resolve, reject) => {
  reject("fail");
});
console.log(promise);

```

给reject()函数传递参数改变的是promise对象rejected的结果。

## promise的方法

### then方法

then方法是1个函数。

#### then方法的参数

then方法的参数是2个函数。

```javascript
var promise = new Promise((resolve, reject) => {
  resolve("succeed");
});
promise.then(
  // 第一个参数函数在promise对象的状态为fulfilled时调用
  () => {
    console.log("call when succeed");
  },
  // 第二个参数函数在promise对象的状态为rejected时调用
  () => {
    console.log("call when fail");
  }
);
```

结果打印"succeed to use"。

```javascript
var promise = new Promise((resolve, reject) => {
  reject("fail");
});
promise.then(
  // 第一个参数函数在promise对象的状态为fulfilled时调用
  () => {
    console.log("call when succeed");
  },
  // 第二个参数函数在promise对象的状态为rejected时调用
  () => {
    console.log("call when fail");
  }
);
```

结果打印"fail to use"。

可以通过给then方法的参数函数传递参数获取promise对象的结果。

```javascript
var promise = new Promise((resolve, reject) => {
  resolve("succeed");
});
promise.then(
  // 第一个参数函数在promise对象的状态为fulfilled时调用
  (value) => {
    console.log("call when succeed", value);
  },
  // 第二个参数函数在promise对象的状态为rejected时调用
  (reason) => {
    console.log("call when fail", reason);
  }
);

```

结果打印"call when succeed succeed"

给then方法的第一个参数函数传递一个value参数，可以获取到resolve("succeed")函数传递进来的参数。

```javascript
var promise = new Promise((resolve, reject) => {
  resolve("succeed");
});
promise.then(
  // 第一个参数函数在promise对象的状态为fulfilled时调用
  (value) => {
    console.log("call when succeed", value);
  },
  // 第二个参数函数在promise对象的状态为rejected时调用
  (reason) => {
    console.log("call when fail", reason);
  }
);

```

结果打印"call when fail fail"

给then方法的第二个参数函数传递一个reason参数，可以获取到reject("fail")函数传递进来的参数。

#### then方法的返回值

then方法的返回值是一个新的promise对象，这个promise对象的状态是pending。

在then方法的参数函数中使用return关键字可以改变then方法返回的新的promise对象的状态。

### catch方法

catch方法的参数是一个函数。

catch方法的参数函数会在以下情况执行。

```
1. 当promise对象的状态为rejected时，catch方法的参数函数执行。

2. 当promise对象执行体中出现代码错误时，catch方法的参数函数执行。
```

```javascript
var promise = new Promise((resolve, reject) => {
  reject("fail");
});

promise.catch((reason) => {
  console.log("error");
});

```

## promise常见写法

```javascript
new Promise((resolve, reject) => {
  // promise的执行体
})
  .then((value) => {
    // promise的状态为fulfilled时执行
    console.log("call when succeed");
  })
  .catch((reason) => {
    // promise的状态为rejected时执行
    console.log("call when fail");
  });
```

<++>
































