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

语法：

```javascript
document.body
```

**获取html元素**

语法：

```javascript
document.documentElement
```

## 事件

事件由三部分组成：**事件源**，**事件类型**，**事件处理程序**。

事件源：事件被触发的对象。

事件类型：如何触发，触发什么事件。

事件处理程序：通过一个函数赋值的方式完成。

**执行事件的步骤**

```
1.获取事件源。
2.注册事件（绑定事件）。
3.添加事件处理程序（采用函数赋值的形式）。
```

## 操作元素

### 改变元素的内容

**element.innerText**从起始位置到终止位置的内容，去除html标签，空格和换行。

**element.innerHTML**从起始位置到终止位置的内容，保留html标签，空格和换行。

例：

```html

<button id="but">点击</button>
<div id="div">xxx</div>

<script>
        var button = document.getElementById('but');
        var div = document.getElementById('div');
        but.onclick = function () {
            div.innerHTML = "hhh";
        }
</script>

// 代码块运行结果为点击按钮，div种的文本“xxx”变为“hhh”
```

### 修改元素属性

例：

```html
	<button id="a">1</button>
    <button id="b">2</button>
    <img src="./images/mimi01.jpg" alt="">

<script>
    var a=document.getElementById('a');
    var b=document.getElementById('b');
    var img =document.querySelector('img');
    a.onclick=function(){
    img.src='./images/mimi01.jpg';
    }
    b.onclick=function(){
    img.src='./images/mimi02.jpg';
    }
</script>

//点击按钮可以切换图片（修改了src属性）
```

#### 按钮点击

```javascript
var flag = 0;
b.onclick = function () {
    if (flag == 0) {
		b.style.backgroundColor = '#FFDEAD';
		flag = 1;
	} else {
		b.style.backgroundColor = '#6495ED';
		flag = 0;
	}
}
// 实现按钮反复点击
```

#### 修改表单属性

修改input元素的属性。

#### 修改样式属性

==element.style==行内样式操作。

==element.className==类名样式操作。

> * js修改style样式操作，产生的是行内样式，css权重比较高。
> * 可以通过修改元素的==className==更改元素的样式。
> * className会直接更改元素的类名，会覆盖原先的类名。

#### 显示隐藏文本框的内容

表单事件：onfocus（获得焦点），onblur（失去焦点）。

```html
<input type="text" value="xxx">
<script>
	var inp=document.querySelector('input');
	inp.onfocus=function(){
	if(this.value=='xxx'){
	inp.value='';
		}
	}
	inp.onblur=function(){
		if(this.value==''){
		inp.value='xxx';
		}
	}
</script>
```

#### 排他思想

如果有同一组元素，需要实现某个元素单一样式，需要使用循环排他思想。

> * 清楚所有元素样式。
> * 设置当前元素的样式。

```html
<button>1</button>
<button>2</button>
<button>3</button>
<button>4</button>
<button>5</button>
<script>
    var btn = document.querySelectorAll('button');
    for (var i = 0; i < btn.length; i++) {
        btn[i].onclick = function () {
            for (var i = 0; i < btn.length; i++) {
                btn[i].style.backgroundColor = '';
            }
            this.style.backgroundColor = '#FFDEAD';
        }
    }
</script>
```

#### 换肤效果

核心算法：把当前图片的src路径取过来，给body作为背景。

```html
<style>
        * {
            margin: 0;
            padding: 0;
        }

        body {
            background: url(./images/IMG_6606.JPG) no-repeat;
        }

        ul {
            width: 364px;
            margin: 160px auto;
        }

        ul li {
            float: left;
            list-style: none;
            border: 1px solid #FAEBD7;
        }

        ul li:nth-child(2) {
            margin-left: -1px;
        }

        ul li img {
            width: 180px;
            vertical-align: -4px;
        }
</style>
```

```html
<ul>
    <li>
        <img src="./images/IMG_6606.JPG">
    </li>
    <li>
        <img src="./images/IMG_6608.JPG">
    </li>
</ul>
<script>
    var bac=document.querySelector('ul').querySelectorAll('img');
    var bod=document.body
    for(var i=0;i<bac.length;i++){
        bac[i].onclick=function(){
            bod.style.background='url('+this.src+')';
        }
    }
</script>
//实现背景图片的切换
```

#### 表格隔行变色效果
