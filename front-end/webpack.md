# Webpack

----------

## 拆分开发环境和生产环境配置

----------

[生产环境](https://webpack.docschina.org/guides/production/)

## 打包的时候不产生 License

----------

参考链接：[https://juejin.cn/post/6935985280784531487](https://juejin.cn/post/6935985280784531487)

使用 Webpack 内置的 `terser-webpack-plugin`。

```js
const TerserPlugin = require('terse-webpack-plugin');

module.exports = {
  // ...
  optimazation: {
    minimizer: {
      new TerserPlugin({
        extractComments: false
      })
    }
  }
}
```
