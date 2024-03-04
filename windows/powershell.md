# PowerShell

----------

[TOC]

## 配置文件

----------

Windows下的配置文件：`$PROFILE`。

## Get-ChildItem

----------

`Get-ChildItem` 命令可以在一个或多个位置获取项目和子项目。

`gci`、`dir` 和 `ls` 都是 `Get-ChildItem` 的别名。

## Get-Location

----------

`Get-Location` 用于获取有关当前工作目录或位置堆栈的信息，类似于 `pwd`。

## Set-Location

----------

`Set-Location` 将当前工作位置设为指定位置。

`sl`、`cd` 和 `chdir` 都是 `Set-Location` 的别名。

## New-Item

----------

`New-Item` 用于在文件系统中创建文件和目录。

创建符号链接到文件：

```powershell
New-Item -ItemType SymbolicLink -Path "link.txt" -Target "target.txt"
```

创建符号链接到目录：

```powershell
New-Item -ItemType SymbolicLink -Path "link_dir" -Target "target_dir" -Force
```
