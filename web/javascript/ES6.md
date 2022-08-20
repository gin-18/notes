# ES6

## let和const

`let`和`const`声明的变量

```
1. 不存在变量提升

2. 暂时性死区

3. 不允许重复声明

4. 块级作用域
```

#### 暂时性死区

只要块级作用域内存在`let`命令，则`let`命令声明的变量就`绑定`在这个区块内，不再受外部影响。

```javascript
var a = 1 ;

{
  console.log(a);
  let a = 2;
}
```

`let`声明的变量`绑定`在这个区块内，区块内的打印语句访问不到外部声明的变量`a`。


## 变量的解构赋值

#### 对象的解构赋值

<++>

## 模板字符串

<++>

## 简化对象写法

<++>

## 箭头函数

箭头函数中this是静态的。

this始终指向函数声明时所在作用域下的this的值。

不能作为构造函数实例化对象。

不能使用`arguments`变量。

省略小括号：只有一个形参时可以省略小括号。

省略大括号：函数中只有一条语句的时候可以省略大括号。

## 允许函数形参赋初始值

<++>

## rest参数

rest参数用于获取函数的实参，rest替代了arguments。

## 扩展运算符

<++>

## symbol数据类型

symbol表示独一无二的值。

## class关键字

```javascript
class Preson {
  // constructor方法
  constructor(uname) {
    this.uname = uname;
  }
  // 定义方法
  run() {
    // ...
  }
}
```

## 继承

```javascript
class Father {
  constructor() {
    // ...
  }
  run() {
    // ...
  }
}

class Son extends Father {
  // ...
}
```

## super关键字

super关键字用于访问和调用父类的函数，父类的构造函数，父类的普通函数。

子类中的super必须放在this的前面。
































