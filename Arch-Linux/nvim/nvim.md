# (neo)vim

## (neo)vim配置文件

(neo)vim的配置文件默认没有创建，需要手动创建。

```
1. vim配置文件的位置在~/.vim目录下。.vim目录需要手动创建。在.vim目录下创建vimrc文件,vimrc就是vim的配置文件。

2. neovim配置文件的位置在~/.config/nvim目录下。nvim目录需要手动创建。在nvim目录下创建init.vim文件，init.vim就是neovim的配置文件。 
```

## 普通模式下的命令(未修改键位)

| 命令                   | 描述                                        |
|------------------------|---------------------------------------------|
| .                      | 重复上一次的修改                            |
| *                      | 可以查找出当前光标下的单词                  |
| s                      | 删除光标下的字符并进入插入模式              |
| b                      | 把光标移动到单词的开头                      |
| f                      | 查找指定字符并移动光标到该字符上            |
| ;                      | 把光标移动到f命令查找结果的下一个字符上     |
| ,                      | 把光标移动到f命令查找结果的上一个字符上     |
| u                      | 撤销上一次的修改                            |
| c                      | 修改操作符                                  |
| C                      | 删除光标之后的所有文本并进出插入模式        |
| d                      | 删除操作符                                  |
| D                      | 删除光标之后的所有文本                      |
| y                      | 复制到寄存器（操作符）                      |
| >                      | 增加缩进                                    |
| <                      | 减少缩进                                    |
| =                      | 自动缩进                                    |
| !                      | 使用外部程序过滤{motion}所跨越的行          |
| ~                      | 反转大小写                                  |
| gu                     | 转换为小写                                  |
| gU                     | 转换为大写                                  |
| zz                     | 把当前行显示在窗口正中间                    |
| ga                     | 查看当前光标下字符的unicode码及其他详细信息 |
| ZZ                     | 保存退出                                    |
| :sav path/fileName.txt | 将本缓冲区保存为文件                        |
| :e!                    | 重载本文件                                  |
| :le                    | 当前行居左对齐                              |
| :ce                    | 当前行居中对齐                              |
| :ri                    | 当前行居右对齐                              |
| cc                     | 删除一行并进入插入模式                      |
| Vu                     | 将当前行改为小写                            |
| VU                     | 将当前行改写为大写                          |
| :term zsh              | 在底部分割一个独立窗口并调用zsh             |
| :. w !zsh              | 将当前行写入zsh                             |
| :3,6 join              | 将3-6行进行合并                             |
| W                      | 跳过标点符号到下一个词的词首                |
| B                      | 跳过标点符号到上一个词的词首                |
| gj                     | 同一行的下一行                              |
| gk                     | 同一行的上一行                              |
| vim -u NONE -N         | 以不加载任何插件的方式启动vim               |
| vim -                  | 命令输出结果进入vim中编辑                   |
| :r !<command>          | 读取命令的输出结果                          |

## tab and space

设置spcae替换tab。

```
:set expandtab
```

设置后，只对新输入的tab有效，使用`retab`或`ret`把之前输入的tab替换成space。

```
:ret

or

:retab
```

## 查找和替换

substitute命令的作用是查找和替换。

```
:<作用范围>s/<目标>/<替换>/<替换标志>
```

#### 作用范围

作用范围分为`当前行`，`全文`，`选区`等等。

当前行

```
:s/<目标>/<替换>/g
```

全文

```
:%s/<目标>/<替换>/g
```

选区

```
:'<,'>s/<目标>/<替换>/g 

// 在可视模式下输入：，vim会自动补全为:'<,'>
```

## 命令行模式

在命令行模式下表示当前目录和当前文件名的方法

```
% : 当前完整的文件名

%:h : 文件名的头部，即文件目录

%:e : 扩展名
```

将vim放在后台：ctrl+z

输入shell命令：fg ; 接入后台的vim

## 折叠

```
zf：创建折叠
zc：折叠
zC：折叠所在范围内所有嵌套的折叠点
zo：展开折叠
zO：展开所在范围内的所有嵌套的折叠点
zd：删除折叠
zD：递归删除光标下的折叠
zE：删除窗口里的所有折叠
```

## 标记

```
创建标记：m + <a-z>
跳转标记：' + <a-z>
列出标记：命令:marks
删除标记：命令:delmarks <a-z>
```

## 插件

### coc

#### 安装依赖

```
1. python3
2. python-pip
3. nodejs
4. npm
```

#### 安装neovim nodejs module

```
sudo npm install -g neovim
```

#### 安装neovim python module

```
pip install --user pynvim
pip3 install --user pynvim
```

ps : 不需要使用sudo命令

### fzf.vim

| 命令           | 描述                      |
|----------------|---------------------------|
| :Files [PATH]  | 查找文件                  |
| :GFiles [OPTS] | 查找git文件(git ls-files) |
| :GFiles?       | git status                |
| :Commands      | 查找命令                  |
| :Maps          | 查找键位映射              |
| :History/      | 查找搜索历史              |

### bracey.vim

写html自动刷新页面

安装

```
Plug 'turbio/bracey.vim'

或

Plug 'turbio/bracey.vim', { 'do': 'npm install --prefix server' }
```

如果报错：Connection refused

```
1. cd ~/.config/nvim/plugged/bracey.vim

2. npm install --prefix server
```

### nerdtree

| 按键 | 描述                       |
|------|----------------------------|
| !    | 执行当前文件               |
| O    | 递归打开选中的目录         |
| x    | 合拢选中节点的父目录       |
| X    | 递归合拢选中节点的所有目录 |
| P    | 跳到根节点                 |
| p    | 跳到父节点                 |
| r    | 递归刷新选中目录           |
| R    | 递归刷新节点               |
| m    | 打开文件系统菜单           |
| I    | 显示隐藏文件               |
| <++> | <++>                       |

## 快捷键操作

| 快捷键    | 描述                       |
|-----------|----------------------------|
| H         | 跳到行首                   |
| L         | 跳到行尾                   |
| Alt+H     | 切换到左分屏               |
| Alt+J     | 切换到下分屏               |
| ALt+K     | 切换到上分屏               |
| Alt+L     | 切换到右分屏               |
| Y         | 可视模式下复制到系统剪贴板 |
| Alt+p     | 从系统剪贴板粘贴           |
| Alt+g     | 打开lazygit                |
| Alt+t     | 打开终端                   |
| leader+nt | 打开一个新标签             |
| Tab+h     | 到上一个标签               |
| Tab+l     | 到下一个标签               |
| leader+sc | 打开拼写检查               |
| leader+gd | 跳转到函数定义的地方       |
| leader+gr | 跳转到报错的地方           |
| leader+k  | 打开文档                   |
| leader+t  | 翻译当前光标下的单词       |
| leader+r  | 翻译并替换光标下的单词     |
| Alt+w     | 输入需要翻译的单词         |
| Alt+r     | 打开ranger                 |
| Alt+f     | fzf搜索文件                |
| Alt+m     | fzf搜索标记                |
| Alt+h     | fzf搜索历史文件            |
| Alt+b     | fzf搜索Buffer              |
| Alt+c     | fzf搜索历史命令            |
| Alt+T     | 打开table-mode             |
| Alt+M     | 打开markdown-preview       |
| Alt+v     | 打开vista                  |
| Alt+V     | 打开vista搜索              |
| Alt+e     | 打开nerdtree               |
| <++>      | <++>                       |
| <++>      | <++>                       |

### 在浮动窗口打开lazygit

```shell
noremap <M-g> :call OpenFloatingWin()<CR>:term lazygit<CR>i

function! OpenFloatingWin()
	let height = &lines - 3
	let width = float2nr(&columns - (&columns * 2 / 10))
	let col = float2nr((&columns - width) / 2)

	let opts = {
		\ 'relative': 'editor',
		\ 'row': height * 0.1,
		\ 'col': col * 1.4,
		\ 'width': width * 9 / 10,
		\ 'height': height * 8 / 10
	  \ }

	let buf = nvim_create_buf(v:false, v:true)
	let win = nvim_open_win(buf, v:true, opts)

	call setwinvar(win, '&winhl', 'Normal:Pmenu')

	setlocal
				\ nonumber
				\ norelativenumber
endfunction
```

## word

```
stdin : 标准输入
```

<++>


## 插件

### markdown preview

---

`GitHub`：[markdown preview](https://github.com/iamcco/markdown-preview.nvim)

### vim-table-mode

---

`GitHub`：[vim-table-mode](https://github.com/dhruvasagar/vim-table-mode)

### coc

---

`GitHub`：[coc.nvim](https://github.com/neoclide/coc.nvim)

### rnvimr

---

`GitHub`：[rnvimr](https://github.com/kevinhwang91/rnvimr)

### dict

---

`GitHub`：[dict.vim](https://github.com/iamcco/dict.vim)

### bracey.vim

---

`GitHub`：[bracey.vim](https://github.com/turbio/bracey.vim)

### fzf

---

`GitHub`：[fzf.vim](https://github.com/junegunn/fzf.vim)

### md-img-paste

---

`GitHub`：[md-img-paste](https://github.com/ferrine/md-img-paste.vim)

### nerdcommenter

---

`GitHub`：[nerdcommenter](https://github.com/preservim/nerdcommenter)

### indent-blankline

---

`GitHub`：[indent-blankline](https://github.com/lukas-reineke/indent-blankline.nvim)

### nvim-treesitter

---

`GitHub`：[nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter)

### vim-surround

---

`GitHub`：[vim-surround](https://github.com/tpope/vim-surround)

### vim-hexokinase

---

`GitHub`：[vim-hexokinase](https://github.com/RRethy/vim-hexokinase)
