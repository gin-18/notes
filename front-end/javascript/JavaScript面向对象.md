# JavaScript 面向对象

---

[TOC]

## 对象的组成

---

对象是由 `属性` 和 `方法` 组成的：

* 对象的 `特征` 称为 `属性`，用 `变量` 表示

* 对象的 `行为` 称为 `方法`，用 `函数` 表示

## 构造函数

---

在 JavaScript 中主要是通过 `构造函数` 和 `原型链` 来模拟 `类`。

构造函数有如下 `两个` 特点：

* 函数体内部使用 `this` 关键字，代表要生成的实例对象

* 实例化对象时，必须使用 `new` 命令

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}
```

## new 命令

---

`new` 命令用于执行构造函数，返回一个实例对象。

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

var person = new Person("xxx", 18);

person.name // "xxx"
person.age // 18
```

### new 命令的原理

---

使用 `new` 命令实例化对象时，构造函数会依次执行以下操作：

1. 创建一个 `空对象`，作为将要返回的实例对象

2. 将这个 `空对象` 的原型，指向构造函数的 `prototype` 属性

3. 将这个 `空对象` 赋值给 `this` 关键字

4. 开始执行构造函数内的代码

## this 关键字

---

`this` 就是 `属性` 或 `方法` 当前所在的对象。

```javascript
var person = {
  name: "xxx",
  describe: function () {
    return "name: "+ this.name;
  }
}

person.describe // name:xxx
```

上面的代码，`name` 属性是在 `person` 对象中定义的，所以 `this.name` 指的就是 `person.name`，因此 `this` 指向 `person`。

由于对象的 `属性` 是可以赋值给 `另一个对象` 的，所以 `属性` 所在的 `当前对象` 是可变的，即 `this` 的指向是可变的。

```javascript
function person_1 = {
  name : "number 1",
  describe: function() {
      return "name: " + this.name;
    }
}

function person_2 = {
    name: "number 2"
}

person_2.describe = person_1.describe;

person_2.describe() // name: number 2
```

上面的代码，`person_1.describe` 属性被赋值给 `person_2.describe`，所以 `person_2.describe` 就表示 `describe` 方法所在的 `当前对象` 是 `person_2`，因此 `this` 就指向 `person_2`。

### this 指向的情形

---

#### 全局环境

---

全局环境下，`this` 指向的是 `window` 对象。

```javascript
function f() {
  consolo.log(this)
}

f() // window
```

上面的代码说明，函数在全局环境下运行，`this` 指向的就是 `window` 对象。

#### 构造函数

---

构造函数中的 `this` 指向的是实例对象。

```javascript
function Person(name) {
  this.name = name;
}

var person_1 = new Person("ming")
var person_2 = new Person("hong")

person_1.name // "ming"
person_2.name // "hong"
```

上面的代码说明，两个实例对象的 `name` 属性不同，所以 `this` 指向的是实例对象本身。

#### 对象的方法

---

对象中的 `this` 指向的是 `方法运行时所在的对象`，但是，如果该方法赋值给另一个对象，就会改变 `this` 的指向。

```javascript
var o = {
  f: function() {
    console.log(this)
  }
}

o.f() // o
```

上面的代码，`方法f` 是由 `对象o` 调用的，所以 `this` 指向的是 `对象o`。

### 绑定 this 的方法

---

JavaScript 提供 `call`、`apply` 和 `bind` 3个方法来切换 `this` 的指向。

#### Function.prototype.call()

---

`call` 方法可以指定函数内部 `this` 的指向，并在所指定的作用域中调用该函数。

`call` 方法 `第一个参数` 是 `this` 所有指向的对象，其后的参数是函数本来的参数。

```javascript
var o = {};

function f(name) {
  console.log(this, name);
}

f("xxx") // window xxx
f.call(o, "xxx") // o xxx
```

#### Function.prototype.apply()

---

`apply` 方法的作用和 `call` 方法类似，唯一不同的是 `apply` 方法函数本来的参数接收的是 `一个数组`。

```javascript

var o = {};

function f(name) {
  console.log(this, name);
}

f("xxx") // window xxx
f.apple(o, ["xxx"]) // o xxx
```

#### Function.prototype.bind()

---

`bind` 方法用于将函数体内部的 `this` 绑定到某个对象，然后返回一个新函数。

```javascript
var person_1 = {
  name: "ming",
  sayMyName: function() {
    console.log(this.name)
  }
}

var person_2 = {
  name: "hong",
}

var f = person_1.sayMyName.bind(person_2);

f() // "hong"
```

## 对象的继承

---

在 `构造函数` 中定义的 `方法` 在 `多个实例` 间是无法共享的。

```javascript
function Person(name) {
  this.name = name;
  this.sayMyName = function () {
    console.log(this.name);
  };
}

var person_1 = new Person("ming");
var person_2 = new Person("hong");

person_1.sayMyName(); // "ming"
person_2.sayMyName(); // "hong"

console.log(person_1.sayMyName === person_2.sayMyName); // false
```

从上面的代码可以看出，`person_1` 和 `person_2` 的 `sayMyName` 方法的比较为 `false`，也就是说，每新建一个实例，就会创建一个 `sayMyName` 方法。相同功能的方法创建了两个，这就造成了资源的浪费。

### prototype 属性

---

JavaScript 中有一个 `原型对象`，`原型对象` 的所有属性和方法都能被实例对象共享。

在 JavaScript 中，每个函数都有一个 `prototype` 属性指向 `一个对象`。

```javascript
function f() {}

typeof f.prototype // Object
```

上面的代码中，`函数f` 默认具有一个 `prototype` 属性，并且其类型为 `Object`。

`prototype` 属性会在构造函数生成实例时，自动成为实例对象的原型。

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.sayMyName = function() {
  console.log(this.name);
}

var person_1 = new Person("ming");
var person_2 = new Person("hong");

console.log(person_1.sayMyName === person_2.sayMyName); // true
```

上面的代码中，将 `sayMyName` 方法定义在构造函数的 `prototype` 属性上，这样实例 `person_1` 和 实例 `person_2` 都能共享 `sayMyName` 方法。

`原型对象` 的作用就是定义 `实例对象共享的属性和方法`。

### 原型链

---

每个对象都有一个 `__proto__` 属性指向自己的 `原型对象(prototype)`。而 `原型对象(prototype)` 也是一个对象，依然存在 `__proto__` 属性指向自己的 `原型对象(prototype)`...以此类推所有对象的原型可以上溯到 `Object.prototype` 上，而 `Object.prototype` 的原型则是 `null`。

`原型链` 就是对象到原型，再到原型的原型...以此类推，直到终点，即 `Object.prototype`，这样形成的一条链。

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.sayMyName = function() {
  console.log(this.name)
};

var person_1 = new Person("ming");

// 实例对象的 __proto__ 属性指向的是构造函数的 prototype
console.log(person_1.__proto__ === Person.prototype) // true

// Person.prototype 是一个对象，其 __proto__ 属性指向的是 Object.prototype
console.log(Person.prototype.__proto__ === Object.prototype) // true

// Object.prototype.__proto__ 指向的则是 null
console.log(Object.prototype.__proto__) // null

```

上面的代码，从 `person_1 -> person_1.prototype -> Object.prototype` 就形成了一条原型链，而 `__proto__` 可以看作连接点，分别指向各自的原型对象。

### constructor 属性

---

`constructor` 属性定义在 `prototype` 对象上，默认指向 `prototype` 对象所在的构造函数。

因为 `constructor` 属性是定义在 `prototype` 对象上的，因此实例对象也继承了这个属性，也指向其构造函数。

```javascript
function Person(name) {
  this.name = name;
}

console.log(Person.prototype.constructor) // Person

var person_1 = new Person("ming");
console.log(person_1.constructor); // Person
```

### instanceof 运算符

---

`instanceof` 运算符返回一个布尔值，表示对象是否为某个构造函数的实例。

```javascript
function Person(name) {
  this.name = name;
}

var person_1 = new Person("ming");

person_1 instanceof Person // true
```

## 参考链接

---

* [https://wangdoc.com/javascript/oop/new](https://wangdoc.com/javascript/oop/new)

* [https://wangdoc.com/javascript/oop/this](https://wangdoc.com/javascript/oop/this)

* [https://wangdoc.com/javascript/oop/prototype](https://wangdoc.com/javascript/oop/prototype)
