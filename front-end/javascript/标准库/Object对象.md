# Object 对象

---

[TOC]

JavaScript 的所有对象都继承自 `Object` 对象，这些对象都是 `Object` 的实例。

`Object` 对象的原生方法分为 `2种`：

* `Object` 本身的方法，即直接定义在 `Object` 对象上的方法。

* `Object` 的实例方法，即定义在 `Object` 原型对象上的方法。

## Object()

---

`Object` 本身是一个函数，可以直接调用，将 `任意值` 转为 `对象`。

```javascript
var num = 1;

Object(num);

typeof num;
```
