# Vue 指令

引入: 

```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

## MVVM

Model: 模型层

View: 视图层

ViewModel: 连接视图和数据的中间件，vue.js就是MVVM中的ViewModel层的实现者

在MVVM架构中，是不允许数据直接和视图通信的，只能通过ViewModel来通信。

ViewModel能够观察数据的变化，并对视图对应的内容进行更新。

ViewModel能够监听视图的变化，并能够同时数据发生改变。

vue.js就是一个MVVM的实现者，vue的核心就是实现了dom监听和数据绑定。

View层展示的不是Model层的数据，而是ViewModel层的数据。由ViewModel层负责与Model层交互。vue完全解偶了View层和Model层，这是前后端分离实现的重要一环。

## mustache

<++>

## Vue指令

### v-text

---

设置标签的文本值。

```html
<h2 v-text="msg"></h2>

// 定义在data字段中
data: {
  msg: "hello"
}
```

### v-html

---

设置标签的innerHTML。

```html
<h2 v-html="msg"></h2>

// 定义在data字段中
data: {
  msg: "hello"
}
```

### v-on

---

为元素绑定事件。

```html
<h2 v-on:click="<fun>"></h2>
<h2 @click="<fun>"></h2>

// 方法定义在methons字段中
methons: {
  <fun>: function() {}
}
```

### v-show

---

根据表达式的真假，切换元素的显示与隐藏。

`v-show`是改变元素的`display`属性。

```html
// 元素不显示
<h2 v-show="<false>">aaa</h2>

// 元素显示
<h2 v-show="<true>">aaa</h2>
```

### v-if

---

根据表达式的真假，切换元素的显示与隐藏。

`v-if`操作的是`dom`。

```html
// 元素不显示
<h2 v-if="<false>">aaa</h2>

// 元素显示
<h2 v-if="<true>">aaa</h2>
```

### v-bind

---

设置元素的属性。

```html
<h2 v-bind:src=""></h2>
<h2 :src=""></h2>
```

### v-for

根据数据生成列表结构。

```html
<h2 v-for="(item,index) in arr">索引：{{ index }}，数组元素：{{ item }}</h2>
```

### v-model

获取和设置表单元素的值(双向数据绑定)









































