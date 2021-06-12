# vim (markdown 编辑器)

github地址：[https://github.com/GIN-509/nvim](https://github.com/GIN-509/nvim)

## 快速输入

在`插入模式(insert-mode)`下，markdown输入快捷键。

| 快捷键  | 描述                           |
|---------|--------------------------------|
| `,` `f` | 查找下一个`<++>`并进入插入模式 |
| `,` `1` | 输入一级标题                   |
| `,` `2` | 输入二级标题                   |
| `,` `3` | 输入三级标题                   |
| `,` `4` | 输入四级标题                   |
| `,` `5` | 输入五级标题                   |
| `,` `6` | 输入六级标题                   |
| `,` `i` | 输入斜体文本                   |
| `,` `s` | 输入粗体文本                   |
| `,` `e` | 输入粗斜体文本                 |
| `,` `d` | 输入删除线                     |
| `,` `p` | 插入图片                       |
| `,` `a` | 插入链接                       |
| `,` `n` | 插入分隔线                     |
| `,` `c` | 插入代码块                     |
| `,` `m` | 使用反引号包裹                 |

在`plugin/markdown-quick-input.vim`文件中可以修改配置。

![markdown-quick-input](./images/markdown-quick-input.gif)

## markdown预览

插件地址：[markdown-preview.nvim](https://github.com/iamcco/markdown-preview.nvim)

| 快捷键    | 描述     |
|-----------|----------|
| `alt` `m` | 打开预览 |

配置中使用`chromium`浏览器作为预览工具。

在`plugin/markdown-preview.vim`文件中可以修改配置。

![markdown-preview](./images/markdown-preview.gif)

## 表格模板

插件地址：[vim-table-mode](https://github.com/dhruvasagar/vim-table-mode)

| 快捷键            | 描述             |
|-------------------|------------------|
| `alt` `shift` `t` | 启动表格模板     |
| `alt` `shift` `r` | 表格模板重新对齐 |

在`plugin/table-mode.vim`文件中可以修改配置。

在`插入模式(insert-mode)`下，输入`mtb`可以快速生成表格。

![markdown-table](./images/markdown-table.gif)

## 从剪贴板插入图片

插件地址：[md-img-paste.vim](https://github.com/ferrine/md-img-paste.vim)

| 快捷键       | 描述           |
|--------------|----------------|
| `leader` `p` | 输入图片的名称 |

![clip-img](./images/clip-img.gif)





















