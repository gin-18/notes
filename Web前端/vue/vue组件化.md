# Vue组件化

## 注册全局组件

```javascript
Vue.component('cpn', {
  template: ~
    <div>
      <p>aaa</p>
    </div>~
})
```

cpn就是组件的标签名。

## 注册局部组件

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

## 组件模板分离

使用script标签

```javascript
<script type="text/x-template" id='cpn'>
  <div>
    <p>aaa</p>
  </div>
</script>

Vue.component('cpn', {
  template: '#cpn',
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

## 组件数据

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

## 组件通信

### 父组件向子组件传递信息

---

`父组件`通过`props`向`子组件`传递数据。

### 子组件向父组件传递信息

---

`子组件`通过`事件`



通过事件向父组件发送消息
