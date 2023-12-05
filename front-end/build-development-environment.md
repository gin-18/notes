# 搭建开发环境

---

[TOC]

## Webpack + Tailwind CSS + material-design-icon

---

官方地址：

* [Webpack](https://github.com/webpack/webpack)

* [Tailwind CSS](https://github.com/tailwindlabs/tailwindcss)

* [material-design-icon](https://github.com/google/material-design-icons)

### 安装依赖

---

```sh
npm i -D webpack webpack-cli webpack-dev-server @babel/core @babel/preser-env babel-loader html-webpack-plugin mini-css-extract-plugin css-loader tailwindcss autoprefixer postcss postcss-loader

npm install material-icons@latest
```

### Postcss 配置

---

创建 `postcss.config.js` 并写入下面内容。

```js
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  }
}
```

### Tailwind CSS 配置

---

创建 `tailwindcss.config.js` 并写入下面内容。

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{html,js}"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

### babel 配置

---

```js
{
  "presets": ["@babel/preset-env"]
}
```

### Webpack 配置

---

创建 `webpack.config.js` 并写入一下内容。

```js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
  mode: "development",
  entry: {
    index: path.resolve(__dirname, "src", "js", "index.js"),
    game: path.resolve(__dirname, "src", "js", "game.js"),
  },
  output: {
    clean: true,
    filename: "js/[name].bundle.js",
    path: path.resolve(__dirname, "dist"),
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
          options: {
            presets: ["@babel/preset-env"],
          },
        },
      },
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, "css-loader", "postcss-loader"],
      },
      {
        test: /\.webp$/,
        type: "asset/resource",
        generator: {
          filename: "static/images/[hash][ext][query]",
        },
      },
      {
        test: /\.mp3$/,
        type: "asset/resource",
        generator: {
          filename: "static/audio/[hash][ext][query]",
        },
      },
      {
        test: /\.(woff|woff2)$/,
        type: "asset/resource",
        generator: {
          filename: "static/font/[hash][ext][query]",
        },
      },
    ],
  },
  plugins: [
    new MiniCssExtractPlugin({
      filename: "css/[name].css",
    }),
    new HtmlWebpackPlugin({
      filename: "index.html",
      template: path.resolve(__dirname, "src", "index.html"),
      favicon: path.resolve(__dirname, "src", "static", "favicon.ico"),
      chunks: ["index"],
    }),
    new HtmlWebpackPlugin({
      filename: "game.html",
      template: path.resolve(__dirname, "src", "game.html"),
      favicon: path.resolve(__dirname, "src", "static", "favicon.ico"),
      chunks: ["game"],
    }),
  ],
  optimization: {
    splitChunks: {
      chunks: "all",
      minSize: 0,
      cacheGroups: {
        vendor: {
          test: /[\\/]node_modules[\\/]/,
          name: "vendors",
          chunks: "all"
        }
      }
    }
  },
  devServer: {
    port: 8000,
    static: path.resolve(__dirname, "dist"),
  },
};
```

### 使用 Tailwind CSS

---

添加下面的内容到主样式文件 `main.css`。

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### 使用样式文件

---

在需要使用样式的页面的脚本文件中添加以下内容：

```js
import 'material-icons/iconfont/material-icons.css';
import 'path/to/main.css';
```

### package.json 配置

---

修改 `package.json` 文件中的 `scripts` 字段为：

```json
"scripts": {
  "dev": "webpack-dev-server --open",
  "build": "webpack --mode production"
},
```
