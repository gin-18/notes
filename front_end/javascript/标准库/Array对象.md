# Array 对象

---

[TOC]

## 静态方法

---

### Array.isArray()

---

`Array.isArray` 方法返回一个布尔值，表示参数是否为数组。

```javascript
let a = [1, 2, 3]

Array.isArray(a) // true
```

## 实例方法

---

### push()

---

`push` 方法用于在数组的末端添加一个或多个元素，并返回添加新元素后的数组长度。

`push` 方法会改变原数组。

```javascript
let a = [1, 2, 3];

a.push(4, 5, 6) // 返回6
a // [1, 2, 3, 4, 5, 6]
```

### pop()

---

`pop` 方法用于删除数组的最后一个元素，并返回该元素。

`pop` 方法会改变原数组。

```javascript
let a = [1, 2, 3]

a.pop() // 返回3
a // [1, 2]
```

### shift()

---

`shift` 方法用于删除数组的第一个元素，并返回该元素。

`shift` 方法会改变原数组。

```javascript
let a = [1, 2, 3]

a.shift() // 返回1
a // [2, 3]
```

### unshift()

---

`unshift` 方法用于在数组的第一个位置添加一个或多个元素，并返回添加新元素后的数组长度。

`unshift` 方法会改变原数组。

```javascript
let a = [1, 2, 3]

a.unshift(-1, 0) // 返回5
a // [-1, 0, 1, 2, 3]
```

### join()

---

`join` 方法以指定参数为分隔符，将所有数组成员连接为一个字符串返回，如果不提供参数，默认使用逗号分隔。

```javascript
let a = [1, 2, 3]

a.join() // 返回"123"
```

### reverse()

---

`reverse` 方法用于颠倒排序数组，返回改变后的数组。

`reverse` 方法会改变原数组。

```javascript
let a = [1, 2, 3]

a.reverse() // [3, 2, 1]
```
