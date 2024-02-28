# Scoop

---

[TOC]

## 安装 scoop

---

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

## 基本使用

---

### 1. bucket(仓库)

---

1. 查看已经添加的仓库。

```dos
scoop bucket list
```

2. 添加仓库。

```dos
scoop bucket add 仓库名
```

**一些仓库**

| 仓库名 | 描述                   |
|--------|------------------------|
| main   | 默认的主要仓库         |
| extras | 常用软件仓库           |
| games  | 一些开源游戏仓库       |
| dorado | 许多适合中国用户的软件 |

### 2. 搜索软件

---

```dos
scoop search 软件名
```

### 3. 安装软件

---

```dos
scoop install 软件名
```

### 4. 更新软件

---

```dos
scoop update 软件名
```

### 5. 卸载软件

---

```dos
scoop uninstall 软件名
```

### 6. 列出已经安装的软件

---

```dos
scoop list
```

### 7. 帮助命令

---

```dos
scoop help
```
