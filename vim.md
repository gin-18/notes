# vim 学习笔记

---

[TOC]


## 查看 vim 的版本

---

`:version` 命令将展示当前运行的 `vim` 的所有相关信息。

## vim 的3种模式

---

vim 中有 `3` 种模式：`命令模式(Command mode)`、`输入模式(Insert mode)` 和 `底线命令模式(Last Line mode)`。

### 命令模式(Command mode)

---

刚刚启动 vim 就进入了命令模式。

### 输入模式(Insert mode)

---

有以下几种方式可以从 `命令模式` 进入 `输入模式`。

| 按键            | 描述                               |
| --------------- | ---------------                    |
| `i`             | 在光标前进入输入模式               |
| `shift` `i`     | 在行首进入输入模式                 |
| `a`             | 在光标后进入输入模式               |
| `shift` `a`     | 在行尾进入输入模式                 |
| `o`             | 在下一行开启新行并进入输入模式     |
| `shift` `o`     | 在上一行开启新行并进入输入模式     |
| `s`             | 删除光标下的字符并进入输入模式     |
| `shift` `s`     | 删除整行并进入输入模式             |
| `shift` `c`     | 删除光标后的所有内容并进入输入模式 |
| `c` `c`         | 删除整行并进入输入模式             |

### 底线命令模式(Last Line mode)

---

在 `命令模式` 下按下 `:` 就可以进入 `底线命令模式`。

以下是保存或退出 vim 的命令。

| 命令            | 描述            |
| --------------- | --------------- |
| `q`             | 退出 vim        |
| `w`             | 保存            |
| `wq`            | 保存并退出 vim  |
| `q!`            | 不保存退出 vim  |

## 命令模式下的操作

---

### 移动光标

---

`<number>` 表示的是数字。

| 按键            | 描述                                       |
| --------------- | ---------------                            |
| `h`             | 光标向左移动一个字符                       |
| `j`             | 光标向下移动到下一行                       |
| `k`             | 光标向上移动到上一行                       |
| `l`             | 光标向右移动一个字符                       |
| `0`             | 光标移动到行首                             |
| `$`             | 光标移动到行尾                             |
| `<number>` `G`  | 光标移动到指定的行                         |
| `g` `g`         | 光标移动到文件的首行                       |
| `shift` `g`     | 光标移动到文件的尾行                       |
| `w`             | 光标移动到下一个词的词首，符号也算作一个词 |
| `shift` `w`     | 光标移动到下一个词的词首，以空白符为间隔   |
| `b`             | 光标移动到上一个词的词首，符号也算作一个词 |
| `shift` `b`     | 光标移动到上一个词的词首，以空白符为间隔   |
| `e`             | 光标移动到下一个词的词尾，符号也算作一个词 |
| `shift` `e`     | 光标移动到下一个词的词尾，以空白符为间隔   |























