# hugo base use

## 建站

```sh
hugo new site <blog_name> # 新建一个站点

cd <blog_name>

git init

git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke # 添加主题

echo "theme = 'ananke'" >> hugo.toml # 设置主题

hugo server # 启动服务
```

## 写文章

```sh
hugo new content content/posts/post.md # 新建文章

hugo server -D # 启动服务
```

## Draft, future, and expired content

Hugo 允许在文章的头部设置 `draft`, `date`, `publishDate` 和 `expiryDate`。

在默认设置中，在下面的情况下，Hugo 不会发布文章：

* draft 的值为 true

* date 的值是将来的时间

* publishDate 的值是将来的时间

* expiryDate 的值是过去的时间

使用下面的命令，可以覆盖默认设置:

```sh
hugo --buildDrafts # or -D

hugo --buildExpired # or -E

hugo --buildFuture # or -F
```

## 查看和测试站点

查看站点布局和内容可以使用一下命令：

```sh
hugo server
```

上面的命令会在内存中运行站点。

## 自动重定向

使用以下命令可以自动重定向到文章页面，当编辑文章的时候:

```sh
hugo server --navigateToChanged
```

## 构建站点

```sh
hugo
```

使用 hugo 命令来构建站点，默认是在 public 目录下。

## 部署站点

TODO: 部署

