# 内置对象

MDN的内置对象文档：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects

内置对象是JavaScript中自带的一些对象，提供一些常用的或最基本的必要功能。

## Math对象

MDN的Math对象：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math

**Math.max()最大值方法**

==Math.max()==方法返回一组数中的最大值。

语法：

```javascript
console.log(Math.max(1, 3, 2));
//输出结果为3
console.log(Math.max(-1, -3, -2));
//输出结果为-1
const array1 = [1, 3, 2];
console.log(Math.max(...array1));
//输出结果为3
```

**Math.abs()绝对值方法**

Math.abs()方法返回一个数字“x”的绝对值。

语法：

```javascript
Math.abs(x);
```

**取整方法**

==Math.floor()==方法返回小于或等于一个给定数字的最大整数（向下取整）。

语法：

```javascript
Math.floor(x);
```

==Math.ceil()==方法返回大于或等于一个给定数字的最小整数（）向上取整。

语法：

```javascript
console.log(Math.ceil(.95));
//输出结果为1
console.log(Math.ceil(4));
//输出结果为4
console.log(Math.ceil(7.004));
//输出结果为8
console.log(Math.ceil(-7.004));
//输出结果为-7
```

==Math.round()==方法返回一个数字四舍五入后最接近的整数。

语法：

```javascript
Math.round(x);
```

> * 四舍六入，遇五取大。

**Math.random()随机数方法**

==Math.random()==方法返回[0,1)区间内的一个浮点，伪随机数，

语法：

```javascript
Math.random();
```

取一个闭区间的随机整数（包含闭区间两侧的整数）

语法：

```javascript
function getRandom(min,max) {
    return Math.floor(Math.random()*(max-min+1)+min);
}
```

#### Date对象

MDN的Date对象：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date

Date对象是一个构造函数，必须使用new来调用创建的对象。

**获取日期的指定部分**

| 方法名                           | 描述             |
| -------------------------------- | ---------------- |
| getFullYear()                    | 获取当年         |
| getMonth()                       | 获取当月（0-11） |
| getDate()                        | 获取当天日期     |
| getDay()                         | 获取星期         |
| getHours()                       | 获取当前小时     |
| getMinutes()                     | 获取当前分钟     |
| getSeconds()                     | 获取当前秒钟     |
| valueOf()，getTime()，Date.now() | 获取时间戳       |

> * 获取时间戳的常用写法：var date = +new Date();

**倒计时**

```javascript
function countDown(time) {
    var currentTime = +new Date();
    var inputTime = +new Date(time);
    var times = (inputTime - currentTime) / 1000;
    var days = parseInt(times / 60 / 60 / 24); //倒计时天数
    days = days < 10 ? '0' + days : days;
    var hours = parseInt(times / 60 / 60 % 24); //倒计时小时
    hours = hours < 10 ? '0' + hours : hours
    var minutes = parseInt(times / 60 % 60); //倒计时分钟
    minutes = minutes < 10 ? '0' + minutes : minutes
    var sceonds = parseInt(times % 60); //倒计时秒钟
    sceonds = sceonds < 10 ? '0' + sceonds : sceonds
    return days + '天' + hours + '时' + minutes + '分' + sceonds + '秒';
}
```

#### 数组对象

MDN的数组对象：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array

==Array.isArray()==用于确定传递的值是否为一个数组。

语法：

```javascript
Array.isArray(obj)
例：
Array.isArray([1, 2, 3]);  // true
Array.isArray({foo: 123}); // false
Array.isArray("foobar");   // false
Array.isArray(undefined);  // false
```

**添加或删除数组元素**

| 方法名            | 描述                                                       | 返回值             |
| ----------------- | ---------------------------------------------------------- | ------------------ |
| push(参数1...)    | 末尾添加一个或多个元素，注意修改原数组                     | 返回新的长度       |
| pop()             | 删除数组的最后一个元素，把数组长度减一。无参数，修改原数组 | 反正删除元素的值   |
| unshift(参数1...) | 向数组开头添加一个或多个元素，注意修改原数组               | 返回新的长度       |
| shift()           | 删除数组的第一个元素，数组长度减一。无参数，修改原数组     | 返回第一个元素的值 |

**数组排序**

| 方法名    | 描述                         | 是否修改原数组               |
| --------- | ---------------------------- | ---------------------------- |
| reverse() | 颠倒数组中的元素顺序，无参数 | 会改变原来的数组，返回新数组 |
| sort()    | 对数组元素进行排序           | 会改变原来的数组，返回新数组 |

**获取数组的索引号**

| 方法名        | 描述                           | 返回值                         |
| ------------- | ------------------------------ | ------------------------------ |
| indexOf()     | 数组中查找给定元素的第一个索引 | 如果存在返回索引号，否则返回-1 |
| lastIndexof() | 在数组中的最后一个索引         | 如果存在返回索引号，否则返回-1 |

**数组去重**

核心算法：先遍历旧数组，再将旧数组元素去查询新数组，如果该元素在新数组中没有则添加，否则不添加。

```javascript
// 数组去重
function unique(arr) {
    var newArr =[];
    for(var i=0;i<arr.length;i++){
        if(newArr.indexOf(arr[i])===-1){
            newArr.push(arr[i]);
        }
    }
    return newArr;
}
console.log(unique([1,1,2,3,5,3,6,7,8,4,5,3])); 
//输出结果为：1，2，3，5，6，7，8，4
```

**数组转换为字符串**

| 方法名         | 描述                               | 返回值         |
| -------------- | ---------------------------------- | -------------- |
| toString()     | 把数组转换为字符串，逗号分隔每一项 | 返回一个字符串 |
| join('分隔符') | 把数组中的索引元素转换成一个字符串 | 返回一个字符串 |

**数组其他常用方法**

| 方法名   | 描述                                                         | 返回值                               |
| -------- | ------------------------------------------------------------ | ------------------------------------ |
| concat() | 用于合并两个或多个数组，不会更改现有的数组                   | 返回一个新数组                       |
| slice()  | 返回一个新的数组对象，这一对象是一个由 begin 和 end 决定的原数组的==浅拷贝==（包括 begin，不包括end）原始数组不会被改变 | 返回一个新的数组对象                 |
| splice() | 通过删除或替换现有元素或者原地添加新的元素来修改数组,并以数组形式返回被修改的内容 | 返回被删除元素的新数组，会修改原数组 |

#### 字符串对象

**基本包装类型**：把基本数据类型包装成复杂数据类型。

字符串的不可变

字符串的不可变指的是值不可变，内存会开辟新地址存放新的字符串，变量指向新的地址。

**根据字符返回位置**

| 方法名                                 | 描述                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| indexOf('要查找的字符',开始查找的位置) | 返回指定内容在原字符串中的位置，如果找不到则返回-1。开始位置是index的索引号 |
| lastIndexOf()                          | 从后往前找，只找第一个匹配的                                 |

**求某个字符出现的位置及次数**

核心算法：先查找第一个字符的位置，找到第一个位置，再使索引号+1，从而继续查找。

```javascript
//求字符出现的位置和次数
var str = 'sducsdbchbsdcjksnjnsjcnjncshdnksjnckJavaScriptd';
var index = str.indexOf('s');
var num = 0;
while (index !== -1) {
    console.log(index);
    num++;
    index = str.indexOf('s', index + 1);
}
console.log('出现次数：' + num);
```

**根据位置返回相应的字符**

| 方法名            | 描述                                        |
| ----------------- | ------------------------------------------- |
| charAt(index)     | 返回指定位置处的字符（index字符串的索引号） |
| charCodeAt(index) | 获取指定字符处的ASCII码（index索引号）      |
| str[index]        | 获取指定位置处字符                          |

**判断一个字符串中出现次数最多字符，并统计次数**

核心算法：利用charAt()遍历整个字符，把每个字符存给一个对象，如果这个对象没有该属性则为1，否则+1。

```javascript
var str2 = 'mdjdcjknkJavaScriptncbusaiwuhujahuiunsidas';
var o = {};
for (var i = 0; i < str2.length; i++) {
    var chars = str2.charAt(i);
    if (o[chars]) {
        o[chars]++;
    } else {
        o[chars] = 1;
    }
}
console.log(o);
var max = 0;
var ch = '';
for (var k in o) {
    if (o[k] > max) {
        max = o[k];
    }
    ch = [k];
}
console.log('出现最多的字符是：' + ch + ';' + '出现的次数是：' + max);
```

**拼接以及截取字符串**

| 方法名               | 描述                                                        |
| -------------------- | ----------------------------------------------------------- |
| concat(str1...)      | 用于连接两个或多个字符串。                                  |
| substr(start,lenght) | 中start位置开始，lenght为取得个数（==重点==）               |
| slice(start,end)     | 从start位置开始，截取到end的位置，end截取不到               |
| substring(start,end) | 从start位置开始，截取到end的位置，end截取不到，不会接受负值 |

**替换字符串以及转换成数组**

| 方法名           | 描述                                                         |
| ---------------- | ------------------------------------------------------------ |
| replace()        |                                                              |
| splice('分隔符') | 使用指定分隔符将一个字符串对象分隔成子字符串数组，以一个指定的分割字串来决定每个拆分的位置 |

