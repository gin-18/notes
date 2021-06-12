# neovim配置 (前端开发)

配置地址：[https://github.com/GIN-509/nvim](https://github.com/GIN-509/nvim)

## 自动补全

插件地址：[coc.nvim](https://github.com/neoclide/coc.nvim)

| 键位             | 描述                       |
|------------------|----------------------------|
| `tab`            | 向下高亮补全项             |
| `shift` `tab`    | 向上高亮补全项             |
| `enter`          | 选择高亮的补全项           |
| `leader` `g` `d` | 跳转到变量或函数定义的地方 |
| `leader` `g` `r` | 跳转到代码错误的地方       |

在`plugin/coc.vim`文件中可以修改配置。

![coc](./images/coc.gif)

## 颜色显示

插件地址：[coc-highlight](https://github.com/neoclide/coc-highlight)

在vim中显示颜色。

![coc-highlight](./images/coc-highlight.png)

## 代码片段

插件地址：[coc-sinppets](https://github.com/neoclide/coc-snippets)

在`UltiSnips`目录下可以添加自定义的代码片段。

例：

添加一个shell脚本的开头的代码片段：`sh.sinppets`。

```sh
snippet sh "shell heading"
#!/bin/bash

# Author: ${1:gin}
# CreateDate: <++>
# Description: <++>

<++>
endsnippet
```

![coc-snippets](./images/coc-snippets.gif)

## 自动刷新页面

插件地址：[bracey.vim](https://github.com/turbio/bracey.vim)

| 快捷键    | 描述       |
|-----------|------------|
| `alt` `i` | 启动bracey |

![bracey](./images/bracey.gif)<++>
