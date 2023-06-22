# JavaScript运算符

---

[TOC]

## 算术运算符

---

### 加法运算符

---

加法运算符 `+` 用来求两个数值的和。

```javascript
1 + 1 // 2
```

加法运算符允许 `非数值` 的相加。

```javascript
true + true // 2
```

上面的代码，两个 `true` 相加，得到的结果为 `2`。

如果是两个 `字符串` 相加的话，会将两个字符串连接并返回。

```javascript
"hello" + "world" // helloworld
```

如果一个运算子是 `字符串`，另一个运算子是 `非字符串`， 这时 `非字符串` 会转成字符串，再连接在一起。

```javascript
1 + "1" // 11
```

### 余数运算符

---

余数运算符 `%` 返回除法运算的 `余数`。

```javascript
3 % 2 // 1
```

需要注意的是，运算结果的正负号是由 `第一个运算子` 的正负号决定的。

```javascript
-3 % 2 // -1

5 % -3 // 2
```

### 自增和自减运算符

---

自增和自减运算符是 `一元运算符`，只需要一个运算子。

自增和自减运算符会将运算子首先转为数值，然后加上 `1` 或减去 `1`，她们会修改原始变量。

```javascript
var a = 1;

a++ // 2

a // 2

a-- // 1

a // 1
```

自增和自减运算符有 `前置` 和 `后置` 之分。

`前置` 时会先进行自增或自减操作，再返回变量操作后的值； `后置` 时会先返回变量操作前的值，再进行自增或自减操作。

```javascript
var b = 1;

// 前置
console.log(++b) // 2
console.log(b) // 2

// 后置
var a = 1;

console.log(a++) // 1
console.log(a) // 2
```

### 指数运算符

---

指数运算符 `**` 完成指数运算，前一个运算子是底数，后一个运算子是指数。

```javascript
2 ** 3 // 8
```

指数运算符是 `右结合`，即多个指数运算符连用时，先进行最右边的计算。

```javascript
2 ** 3 ** 3

相当于

2 ** (3 ** 3)
```

### 赋值运算符

---

赋值运算符 `=` 用于给变量赋值。

```javascript
var a = 1;
```

赋值运算符还可以和其他运算符结合：

```javascript
x += y 等同于 x = x + y

x -= y 等同于 x = x - y

x *= y 等同于 x = x * y

x /= y 等同于 x = x / y

x %= y 等同于 x = x % y

x **= y 等同于 x = x ** y
```

## 比较运算符

---

比较运算符用于比较两个值的大小，然后返回一个布尔值，表示是否满足指定的条件。

```javascript
1 > 2 // false
```

JavaScript 提供 `8种` 比较运算符：

* `>` 大于运算符

* `<` 小于运算符

* `>=` 大于等于运算符

* `<=` 小于等于运算符

* `==` 相等运算符

* `===` 严格相等运算符

* `!=` 不相等运算符

* `!==` 严格不相等运算符

比较运算符可以分为 `2类`：

* `相等比较`

* `非相等比较`

### 非相等运算符：字符串比较

---

这两者的规则不同，对于 `非相等比较` 先判断两个运算子是否为 `字符串`。如果是，就按照 `Unicode` 码点比较；否则，将两个运算子转成数值，再比较数值的大小。

```javascript
"cat" > "dog" // false
```

上面的代码，JavaScript 引擎会首先比较 `首字符的Unicode码点`。如果相等，再比较 `第二个字符的Unicode码点`，以此类推。

### 非相等运算符：非字符串的比较

---

如果两个运算子都是原始类型的值，则先转成数值再比较。

```javascript
2 > "3" // false

等同于

2 > Number("3")
```

### 严格相等运算符

---

严格相等运算符 `===` 比较两个值是否为 `同一个值`，如果两个值不是同一类型，则直接返回 `false`。

```javascript
1 === "1" // false
```

### 相等运算符

---

相等运算符 `==` 在比较两个不同类型的值时，如果都是原始类型的值，则会先转成数值再进行比较。

```javascript
1 == "1" // true
```

上面的代码，`字符串1` 会先转成 `数值` 类型再比较，所以，返回 `true`。

### 严格不相等运算符

---

严格不相等运算符 `!==` 就是 `严格相等运算符` 的结果，然后返回相反值。

```javascript
1 !== "1" // true

等同于

!(1 === "1")
```

### 不相等运算符

---

不相等运算符 `!=` 就是 `相等运算符` 的结果，然后返回相反值。

```javascript
1 != "1" // false

等同于

!(1 == "1")
```

## 布尔运算符

---

### 取反运算符

---

取反运算符 `!` 用于将布尔值变为相反值。

```javascript
!true // false
```

### 且运算符

---

且运算符 `&&` 如果第一个运算子的布尔值为 `true`，则返回第二运算子的值；如果第一个运算子的布尔值为 `false`，则直接返回第一个运算子的值，不再求第二个运算子的值。

```javascript
false && true // false

true && false // false

true && true // true
```

### 或运算符

---

或运算符 `||`，如果第一个运算子的布尔值为 `true`，则返回第一个运算子的值，不再求第二个运算子的值；如果第一个运算子的布尔值为 `false`，则返回第二个运算子的值。

```javascript
true || false // true

false || true // true

false || false // false
```

## 参考连接

---

* [https://wangdoc.com/javascript/operators/arithmetic](https://wangdoc.com/javascript/operators/arithmetic)

* [https://wangdoc.com/javascript/operators/comparison](https://wangdoc.com/javascript/operators/comparison)

* [https://wangdoc.com/javascript/operators/boolean](https://wangdoc.com/javascript/operators/boolean)
