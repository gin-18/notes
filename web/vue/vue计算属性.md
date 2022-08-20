# vue 计算属性

```javascript
new Vue({
  el: "#root",
  data: {
    firstName: "张",
    lastName: "三",
  },
  computed: {
    fullName: {
      get() {
        return this.firstName + "-" + this.lastName;
      },
    },
  },
});
```

当读取计算属性时，`get()`就会被调用，且返回值就作为计算属性的值。

`get()`被调用的时间：

```
1. 初次读取计算属性时。如果依赖的数据未改变，之后读取计算属性是从缓存中读取数据。

2. 所依赖的数据发生变换时。例如，以上代码中的firstName和lastName。
```

## 计算属性简写

属性只读取，不修改的时候才能简写。即只有`get()`函数。

```javascript
computed: {
  fullName() {
    return this.firstName + "-" + this.lastName;
  },
},
```
