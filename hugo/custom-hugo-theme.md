# 制作自己的Hugo主题

## 主题名

hugo-theme-starry 星空的主题

## 需要的功能

* 基本功能：logo, 导航栏，主页，文章列表页，分类页，项目页

* 暗黑模式

* 多语言

* 图片处理

* 底部导航栏的社交媒体链接

* lighthouse评分

* 代码复制

## 项目结构

使用 `hugo new theme <theme_name>` 命令创建一个主题。

默认生成的目录结构如下：

```tree
.
├── archetypes
│   └── default.md
├── assets
│   ├── css
│   │   └── main.css
│   └── js
│       └── main.js
├── content
│   ├── _index.md
│   └── posts
│       ├── _index.md
│       ├── post-1.md
│       ├── post-2.md
│       └── post-3
│           ├── bryce-canyon.jpg
│           └── index.md
├── data
├── hugo.toml
├── i18n
├── layouts
│   ├── _default
│   │   ├── baseof.html
│   │   ├── home.html
│   │   ├── list.html
│   │   └── single.html
│   └── partials
│       ├── footer.html
│       ├── head
│       │   ├── css.html
│       │   └── js.html
│       ├── header.html
│       ├── head.html
│       ├── menu.html
│       └── terms.html
├── LICENSE
├── public
│   ├── categories
│   │   ├── index.html
│   │   └── index.xml
│   ├── css
│   │   └── main.css
│   ├── favicon.ico
│   ├── index.html
│   ├── index.xml
│   ├── js
│   │   └── main.js
│   ├── posts
│   │   ├── index.html
│   │   ├── index.xml
│   │   ├── post-1
│   │   │   └── index.html
│   │   ├── post-2
│   │   │   └── index.html
│   │   └── post-3
│   │       ├── bryce-canyon.jpg
│   │       └── index.html
│   ├── sitemap.xml
│   └── tags
│       ├── blue
│       │   ├── index.html
│       │   └── index.xml
│       ├── green
│       │   ├── index.html
│       │   └── index.xml
│       ├── index.html
│       ├── index.xml
│       └── red
│           ├── index.html
│           └── index.xml
├── README.md
├── static
│   └── favicon.ico
└── theme.toml
```
