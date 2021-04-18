# 闭包

如果内部函数使用了外部函数的变量，就会形成闭包。闭包保留了外部函数环境的引用。

如果内部函数被返回到了外部函数的外面，在外部函数执行完后，依然可以使用闭包里的值。

## 闭包的形成

在内部函数使用外部函数的变量，就会形成闭包。闭包是当前作用域的延伸。

从代码的角度看，闭包也是一个对象。

在内部函数中使用了外部函数的变量，这个变量就会作为闭包对象的属性。

```javascript
function a() {
  var aa = 16;
  function b() {
    console.log(b); // 形成闭包
  }
  b();
}
a();

1. 产生aAO对象。
   aAO：{aa: 16, b: fun}

2. 产生bAO对象。
   bAO: {}

3. [[scopes]] - 0: bAO
                1: aAO
                2: GO
```

## 闭包的保持

如果希望在函数调用之后，闭包仍然保持，就需要将内部函数返回到外部函数的外部。

```javascript
function a() {
  var num = 0;
  function b() {
    console.log(num++); // 形成闭包
  }
  return b;
}
var demo = a();
demo(); // 相当于b() 0
demo(); // 新产生一个bAO，1

1. GO: {demo: undefined, a: fun}

2. aAO: {num: 0, b: fun}

3. 返回b函数给demo，b函数并没有执行。

4. bAO: {}

5. [[scopes]] - 0: bAO
                1: aAO
                2: GO
```

## 闭包的应用

解决函数外部无法访问函数内部变量的问题。

有时不注意使用了闭包，会导致意想不到的结果。

```
1. 在函数外部访问私有变量。

2. 实现封装。

3. 防止全局变量的污染。
```

```javascript
function Person() {
  var uname;
  function setName(uname) {
    this.uname = uname;
  }
  function getName() {
    return this.uname;
  }
  return {
    getName: getName;
    setName: setName;
  }
}

var xiaoming = new Person();
xiaoming.setName("xiaoming");
console.log(xiaoming.getName());
```
