# vue


引入: <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

## MVVM

Model: 模型层

View: 视图层

ViewModel: 连接视图和数据的中间件，vue.js就是MVVM中的ViewModel层的实现者

在MVVM架构中，是不允许数据直接和视图通信的，只能通过ViewModel来通信。

ViewModel能够观察数据的变化，并对视图对应的内容进行更新。

ViewModel能够监听视图的变化，并能够同时数据发生改变。

vue.js就是一个MVVM的实现者，vue的核心就是实现了dom监听和数据绑定。

View层展示的不是Model层的数据，而是ViewModel层的数据。由ViewModel层负责与Model层交互。vue完全解偶了View层和Model层，这是前后端分离实现的重要一环。

## Vue组件化

### 注册全局组件的语法糖

```javascript
Vue.component('cpn', {
  template: ~
	  <div>
		  <p>aaa</p>
		</div>~
})
```

cpn就是组件的标签名。

### 注册局部组件的语法糖

```javascript
var vue = new Vue({
  el: '#app',
	data: {
	  message: 'hello,Vue!'
	},
	components: {
	  cpn: {
		  template: ~
			<div>
			  <p>aaa</p>
			</div>~
		}
	}
})
```

### 组件模板分离

使用script标签

```javascript
<script type="text/x-template" id='cpn'>
  <div>
	  <p>aaa</p>
	</div>
</script>

Vue.component('cpn', {
  template: '#cpn'
})
```

使用template标签

```javascript
<template id="cpn">
  <div>
	  <p>aaa</p>
	</div>
</template>

Vue.component('cpn', {
  template: '#cpn'
})
```

### 组件数据的存放

组件对象也有一个data属性。

data属性必须是一个函数，因为函数每次调用都会在内存中开辟一个新地址。如果是对象的话是同一个地址。

函数返回一个对象，返回的对象内部保存数据。

```javascript
<template id="cpn">
  <div>
	  <p>{{ message }}</p>
	</div>
</template>

Vue.component({
  template: '#cpn',
	data() {
	  reture {
		  message: 'hello'
		}
	}
})
```

### 父子组件的通信

通过props向子组件传递数据

通过事件向父组件发送消息

### 全局组件和局部组件

在vue实例中定义的组件就是局部组件，components属性。

### 父组件和子组件

在父组件中注册子组件，则定义了components属性的组件构造器为父组件。

## ES6模块化

<++>
