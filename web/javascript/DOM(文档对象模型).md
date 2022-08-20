# DOM笔记

## Web API

MDN的Web API参考参考文档：https://developer.mozilla.org/zh-CN/docs/Web/API

API是为程序员提供的一个接口，帮助实现某种功能，会使用即可，不需要知道接口是怎么实现的。

Web API是浏览器提供的一套操作浏览器功能和页面元素的API（BOM和DOM）

JavaScript基础学习的是ECMAscript基础语法。Web API是JavaScript的应用，会大量使用JavaScript基础语法做页面交互效果。

## DOM

DOM是文档对象模型，用于处理可扩展标记语言（HTML或XML）的标准编程接口。

文档：一个页面就是一个文档，DOM中使用document表示。

元素：页面中的所有标签都是元素，DOM中使用element表示。

节点：网页中的所有内容的是节点（标签，属性，文本，注释等）。DOM中使用node表示。

DOM可以把以上内容都看作对象。

## 获取元素

使用console.dir()打印返回的元素对象，更好的查看里面的属性和方法。

**根据ID获取元素**

使用getElementById('id名')方法可以获取带有ID属性的元素对象。

**根据标签名获取元素**

使用getElementsByTagName('标签名')方法可以返回带有指定标签名的对象集合。

**根据类名获取元素**

使用getElementsByClassName('类名')方法可以

**根据选择器获取元素**

使用querySelector('选择器')方法可以返回指定选择器的第一个元素。

使用querySelectorAll('选择器')方法可以返回指定选择器的所有元素对象的集合。

**获取body元素**

```javascript
document.body
```

**获取html元素**

```javascript
document.documentElement
```

## 事件

事件由三部分组成：**事件源**，**事件类型**，**事件处理程序**。

事件源：事件被触发的对象。

事件类型：如何触发，触发什么事件。

事件处理程序：通过一个函数赋值的方式完成。

## 节点

利用节点的层级关系获取元素。

网页中的所有内容都是节点(标签，属性，文本，注释等)，在DOM中，节点使用node表示。

节点至少拥有nodeType(节点类型)，nodeName(节点名称)，nodeValue(节点值)这3个属性。

nodeType(节点类型)

```
元素节点：nodeType为1

属性节点：nodeType为2

文本节点：nodeType为3
```

一般操作的是元素节点。

### 节点层级

父级节点

```
node.parentNode
```

获取的是最近的父级节点。

### 子节点

获取所有的子节点，包括元素节点，属性节点等。

```
parentNode.childNodes
```

只获取元素子节点。

```
parentNode.children

或

parentNode.children[0] //获取第一个子节点
```

获取第一个元素子节点。

```
parentNode.firstElementChild
```

### 兄弟节点

获取下一个元素兄弟节点。

```
node.nextElementSibling
```

获取上一个元素兄弟节点。

```
node.previousElementSibling
```

### 创建节点

```
document.createElement('tagName')
```

### 添加节点

node.appendChild()方法将一个节点添加到指定父节点的子节点列表末尾。

```
node.appendChild(child)
```

```html
<div class="box"></div>
<script>
  var box = document.queryselector(".box");
  var p = document.createelement("p");
  box.appendchild(p);
</script>
```

上面代码会在div标签中添加一个p标签。

node.insertBefore()方法将一个节点添加到父节点指定的子节点的前面。

```
node.insertBefore(child, 指定元素)
```

### 删除节点

node.removeChlid()方法从DOM中删除一个子节点，返回删除的子节点。

```
node.removeChlid(child)
```

### 克隆节点

node.cloneNode()方法返回调用该方法的节点的一个副本。也称克隆节点或拷贝节点。

如果node.cloneNode()的参数为空或false，则是**浅拷贝**，即只克隆节点本身，不克隆里面的子节点。

如果node.cloneNode()的参数为true，则为**深拷贝**，克隆标签中的内容。

```
node.cloneNode()
```

## 事件高级

### 事件监听

```
eventTarget.addEventListener(type, listener[, useCapture]);
```

addEventListener()方法接收3个参数。

```
type：事件的类型(字符串)

listener：事件处理函数，事件发生时会调用监听的函数

useCapture：？？？
```

### 删除事件(解绑事件)

```
eventTarget.removeEventListener(type, listener[, useCapture]);
```

## DOM事件流

事件流是描述页面接收事件的顺序。

事件发生时候在元素节点之间按照特定的顺序传播，这个传播过程就是DOM事件流。

DOM事件流分为3个阶段。

```
1. 捕获阶段

2. 当前目标阶段

3. 冒泡阶段
```

## 事件对象

```
eventTarget.addEventListener('click', function(event){})
```

参数event就是事件对象，一般写成e

event对象代表事件的状态，就是跟事件相关的一系列信息数据的集合，事件对象拥有许多属性和方法。

### 事件对象常见属性和方法

| 事件对象属性和方法  | 描述                          |
|---------------------|-------------------------------|
| e.type              | 返回事件的类型，比如click     |
| e.srcElement        | 返回触发事件的对象，ie6-8使用 |
| e.target            | 返回触发事件的对象            |
| e.returnValue       | 阻止默认事件，ie6-8使用       |
| e.preventDefault()  | 阻止默认事件                  |
| e.cancelBubble      | 阻止冒泡，ie6-8使用           |
| e.stopPropagation() | 阻止冒泡                      |

## 阻止冒泡

利用事件对象中的stopPropagation()方法。

```
stopPropagation()
```

## 事件委托

不是给每个子节点单独设置事件监听器，而是事件监听器设置在父节点上，然后利用冒泡原理影响设置的每个子节点。

## 鼠标事件对象

| 鼠标事件对象 | 描述                                  |
|--------------|---------------------------------------|
| e.clientX    | 返回鼠标相对于浏览器窗口可视区的X坐标 |
| e.clientY    | 返回鼠标相对于浏览器窗口可视区的Y坐标 |
| e.pageX      | 返回鼠标相对于文档页面的X坐标         |
| e.pageY      | 返回鼠标相对于文档页面的Y坐标         |
| e.screenX    | 返回鼠标相对于电脑屏幕的X坐标         |
| e.screenY    | 返回鼠标对象于电脑屏幕的Y坐标         |

## 键盘事件

| 键盘事件   | 描述                               |
|------------|------------------------------------|
| onkeyup    | 按键松开时触发                     |
| onkeydown  | 按键按下时触发                     |
| onkeypress | 按键按下时触发，但是不能识别功能键 |

这3个事件的执行顺序：onkeydown -- onkeypress -- onkeyup

## 键盘事件对象

| 键盘事件对象 | 描述              |
|--------------|-------------------|
| keyCode      | 返回键位的ASCII值 |

onkeyup和onkeydown是不区分字母大小写的，onkeypress区分字母大小写。




















