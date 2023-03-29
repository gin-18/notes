# JavaScript 数据类型转换

---

[TOC]

## 强制转换

---

强制转换主要是指使用 `Number()`、`String()` 和 `Boolean()` 三个函数，手动将各种类型的值分别转换为 `数值`、`字符串` 或 `布尔值`。

### Number()

---

`Number` 函数可以将任意类型的值转换为 `数值`。

对于 `原始类型的值` 转换规则如下：

* 数值：保持原来的值

* 字符串：如果可以解析成数值，则转换成对应的数值；如果不能解析成数值，则返回 `NaN`；`空字符串` 转换为 `0`

* 布尔值：`true` 转换为 `1`；`false` 转换为 `0`

* undefined：转换为 `NaN`

* null：转换为 `0`

```javascript
Number(123) // 123

Number("123") // 123
Number("123xx") // NaN
Number("") // 0

Number(true) // 1
Number(false) // 0

Number(undefined) // NaN

Number(null) // 0
```

### String()

---

`String` 函数可以将任意类型的值转换为 `字符串`。

对于 `原始类型的值` 转换规则如下：

* 数值：转换为对应的字符串

* 字符串：转换为原来的值

* 布尔值：`true` 转换为 `"true"`；`false` 转换为 `"false"`

* undefined：转换为 `"undefined"`

* null：转换为 `"null"`

```javascript
String(123) // "123"

String("123") // "123"

String(true) // "true"
String(false) // "false"

String(undefined) // "undefined"

String(null) // "null"
```

### Boolean()

---

`Boolean` 函数可以将任意类型的值转换为 `布尔值`。

`Boolean` 函数的转换规则如下：除了以下 `5个值` 转换为 `false`，其他都是 `true`。

* undefined

* null

* 0

* NaN

* ""

```javascript
Boolean(undefined) // false
Boolean(null) // false
Boolean(0) // false
Boolean(NaN) // false
Boolean("") // false
```

## 自动转换

---

以下 `3种` 情况，JavaScript会自动转换数据类型。

1. 不同类型的数据相互运算

```javascript
123 + "123" // 123123
```

2. 对于 `非布尔值` 的数据 `求布尔值`

```javascript
if ("xxx") {
  console.log(true)
} // true
```

3. 对 `非数值` 类型的值使用 `一元运算符(+ 和 -)`

```javascript
+ [1, 2, 3] // NaN
```

### 自动转换为布尔值

---

除了以下 `五个值`，其他全部转换为 `true`。

* undefined

* null

* 0

* NaN

* ""

### 自动转换为字符串

---

字符串的紫自动转换，主要发生在字符串的加法运算中。

当一个值是字符串，另一个值是非字符串，则后者转换为字符串。

```javascript
"1" + 1 // 11

"1" + true // 1true
"1" + false // 1false

"1" + undefined // 1undefined

"1" + null // 1null
```

### 自动转换为数值

---

除了 `加法运算符(+)` 有可能将运算子转换为字符串，其他运算符都会把运算子自动转换为数值。

```javascript
"1" - "1" // 0

true - 1 // 0

"a" - 1 // NaN

undefined - 1 // NaN

null - 1 // 0
```

`undefined` 转换为数值时为 `NaN`；`null` 转为数值时为 `0`。

## 参考链接

---

[https://wangdoc.com/javascript/features/conversion](https://wangdoc.com/javascript/features/conversion)
