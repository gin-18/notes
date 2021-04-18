# 预编译

javascript在被解析之前，js解析引擎首先会把整个文件进行预处理，以消除一些歧义。这个过程就叫做预编译。

## 全局对象(global object)

在浏览器环境中，js引擎会整合script标签中的内容，产生window对象，这个window对象就是全局对象。

在node环境中，会产生global对象。

### 全局变量

在script标签中声明的变量为"全局变量"，全局变量作为window对象的属性存在。

```javascript
var a = 100;

console.log(a); // 100

console.log(window.a); // 100
```

打印a变量实际上相当于打印window对象的a属性。

### 全局函数

在script标签中声明的函数为"全局函数"，全局函数作为window对象的方法存在。

```javascript
console.dir(<function>) // 打印函数的内部结构
```

## 活动对象(Activation Object)

在函数调用时产生，用来保存当前函数内部的执行环境，也称为"执行期上下文"。

在函数调用结束时销毁。

如果函数没有执行，那就不会产生AO对象，则在函数中定义的局部变量和局部函数也不会存在，所以不能在函数外部访问函数内部声明的变量和函数。

### 局部变量

在函数内部声明的变量称为"局部变量"，局部变量作为AO对象的属性存在。

```javascript
function a() {
  var i = 0;
  console.log(i);
}

a();
```

只有在函数调用时，才会产生AO对象。

### 局部函数

在函数内部声明的函数称为"局部函数"，局部函数作为AO对象的方法存在。

## 全局预编译

### 流程

```
1. 查找变量声明，作为GO对象的属性名，值为Undefined。

2. 查找函数声明，作为GO对象的属性名，值为function。
```

**变量声明**

```javascript
var a; // 变量声明

var a = 16; // 变量声明+变量赋值
```

**函数声明**

通过function关键字声明函数。

```javascript
function a() {} // 函数声明

var a = function () {}; // 函数表达式，不是函数声明
```

```javascript
console.log(a); // function
var a = 100;
console.log(a); // 100
function a() {
  console.log(16);
}
a(); // 报错，a的值不是一个函数

代码预编译过程：

1. 产生window对象。

2. 查找变量声明，把a作为window对象的属性名，值为Undefined。

3. 查找函数声明，把函数名a作为window对象的属性名，值为function。

4. 全局预编译结束，代码从上到下依次执行。
```

如果存在同名变量和函数，函数的优先级更高。

## 函数预编译

### 流程

```
1. 在函数调用时，为当前函数产生AO对象。

2. 查找形参和变量声明作为AO对象的属性名，值为Undefined。

3. 使用实参的值改变形参的值。

4. 查找函数声明，把函数名作为AO对象的属性名，值为function。
```

```javascript
function a(test) {
  var i = 0;
  function b() {
    console.log(16);
  }
  b();
}
a(16);

代码执行过程：

1. 产生window对象。

2. GO：(1) 查找变量声明。
       (2) 查找函数声明，把函数名a作为GO对象的属性名，值为function。

3. 全局预编译结束。

4. 执行代码。调用a()，产生AO对象。

5. AO：(1) 查找形参test，局部变量i作为AO对象的属性名，值为Undefined。
       (2) 查找实参16，赋值给形参test。
       (3) 查找局部函数b，把函数名b作为AO对象的属性名，值为Undefined。

6. 函数预编译结束。

7. 执行。
```

只要声明了局部函数，函数的优先级最高。

没有声明局部函数，实参的优先级高。

整体来说：局部函数 > 实参 > 形参。
