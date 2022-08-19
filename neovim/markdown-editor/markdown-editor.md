# :black_nib:(Neo)Vim - Markdown Editor

---

`GitHub` address: [GIN-18/nvim](https://github.com/GIN-18/nvim)

## Quick Insert

---

在 `插入模式(insert-mode)` 下，`markdown` 文件中输入:

| Shortcut | Action         |
|----------|----------------|
| `h1`     | 输入一级标题   |
| `h2`     | 输入二级标题   |
| `h3`     | 输入三级标题   |
| `h4`     | 输入四级标题   |
| `h5`     | 输入五级标题   |
| `h6`     | 输入六级标题   |
| `pic`    | 插入图片       |
| `blo`    | 插入代码块     |
| `mar`    | 使用反引号包裹 |
| `tab`    | 插入表格       |
| `link`   | 插入链接       |
| `line`   | 插入分隔线     |
| `,` `i`  | 输入斜体文本   |
| `,` `s`  | 输入粗体文本   |
| `,` `e`  | 输入粗斜体文本 |
| `,` `d`  | 输入删除线     |

在 `UltiSnips/markdown.snippets` 文件中可以修改配置。

![markdown-quick-input](./images/markdown-quick-input.gif)

## :eyeglasses: Markdown Preview

---

plugin address : [iamcco/markdown-preview.nvim](https://github.com/iamcco/markdown-preview.nvim)

| Shortcut    | Action         |
|-------------|----------------|
| `shift` `r` | toggle preview |

配置中使用 `chromium` 浏览器作为预览工具。

在 `plugin/markdown-preview.vim` 文件中可以修改配置。

![markdown-preview](./images/markdown-preview.gif)

## :page_facing_up: Table Mode

---

plugin address : [dhruvasagar/vim-table-mode](https://github.com/dhruvasagar/vim-table-mode)

| Shortcut          | Action            |
|-------------------|-------------------|
| `alt` `shift` `t` | toggle table mode |
| `alt` `shift` `r` | 表格模板重新对齐  |

在 `plugin/table-mode.vim` 文件中可以修改配置。

![markdown-table](./images/markdown-table.gif)

## :camera: Insert Image From Clipboard

---

plugin address : [ferrine/md-img-paste.vim](https://github.com/ferrine/md-img-paste.vim)

| Shortcut     | Action         |
|--------------|----------------|
| `leader` `p` | 输入图片的名称 |

![clip-img](./images/clip-img.gif)




















