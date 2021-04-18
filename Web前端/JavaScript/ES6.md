# ES6

## let和const

`let`声明的变量具有块级作用域，而且变量不能重复声明。

`let`声明的变量不会产生`变量提升`。

`const`声明常量，一般常量大写，常量的值不能修改。

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
































