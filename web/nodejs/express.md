# express

---

[TOC]

## 安装

---

```
npm install -D express
```

## 基本路由

---

```js
// 引入 express
const express = require("express")

// 创建app实例
const app = express()

// 创建路由
app.get('/url', (req, res)=>{
    function content
})
```

## 中间件

---

创建路由时，第二个参数就是中间件。

```js
app.get('/url', [func1, func2, ...])
```

`express` 可使用以下几种中间件：

- 应用级中间件
- 路由级中间件
- 错误处理中间件
- 内置中间件
- 第三方中间件

### 应用级中间件

---


































