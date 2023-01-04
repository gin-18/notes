# :computer: Windows 配置

----------

[TOC]

## Windows Terminal

----------

### 操作

----------

| 快捷键         | 描述                   |
| -------------- | --------------         |
| `alt` `enter`  | 新建标签页             |
| `alt` `c`      | 关闭标签页             |
| `alt` `h`      | 上一个标签页           |
| `alt` `l`      | 下一个标签页           |
| `alt` `f`      | 切换全屏               |
| `alt` `number` | 切换到对应数字的标签页 |
| <++>           | <++>                   |


### 主题

----------

#### Nord

----------

```json
{
  "background": "#2E3440",
  "black": "#3B4252",
  "blue": "#81A1C1",
  "brightBlack": "#4C566A",
  "brightBlue": "#81A1C1",
  "brightCyan": "#8FBCBB",
  "brightGreen": "#A3BE8C",
  "brightPurple": "#B48EAD",
  "brightRed": "#BF616A",
  "brightWhite": "#ECEFF4",
  "brightYellow": "#EBCB8B",
  "cursorColor": "#FFFFFF",
  "cyan": "#88C0D0",
  "foreground": "#D8DEE9",
  "green": "#A3BE8C",
  "name": "Nord",
  "purple": "#B48EAD",
  "red": "#BF616A",
  "selectionBackground": "#2E3440",
  "white": "#E5E9F0",
  "yellow": "#EBCB8B"
}
```

## Scoop

----------

### 安装

----------

`GitHub` 地址 : [ScoopInstaller/Scoop](https://github.com/ScoopInstaller/Scoop)

1. 设置 `PowerShell` 的执行策略。

```dos
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

2. 下载安装脚本到本地。

```dos
irm get.scoop.sh -outfile 'install.ps1'
```

3. 执行安装脚本，`scoop` 会被安装在 `D:\Scoop` 中。

```dos
.\install.ps1 -ScoopDir 'D:\Scoop' -NoProxy
```

4. `D:\Scoop` 目录中子目录的作用。

```
apps：所有通过scoop安装的软件都放在这个目录中。

buckets：scoop软件仓库。

cache：安装包暂存目录。

persit：存储一些用户数据。

shims：用于软连接应用。
```









