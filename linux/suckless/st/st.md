# st

suckless官网：[suckless.org](https://suckless.org/)

[TOC]

## 1. 安装 xorg + base-devel + git

```sh
sudo pacman -S xorg base-devel git
```

## 2. 克隆源码

```sh
git clone https://git.suckless.org/st
```

修改`config.mk`文件。

```sh
# 进入st目录
cd st

# 修改config.mk文件
X11INC = /usr/X11R6/include               X11INC = /usr/include/X11
                                 ->
X11LIB = /usr/X11R6/lib                   X11LIB = /usr/lib/X11
```

## 3. 编译安装

使用源码安装，每次`修改源码`都需要`重新编译安装`。

```sh
# 编译安装
sudo make clean install
```

## 4. st配置

每次编译安装都会根据`config.def.h`文件产生`config.h`文件。

所以可以通过`config.def.h`文件配置`st`。

每次修改源码都需要重新编译安装：

```sh
rm -rf config.h && sudo make clean install
```

## 5. st补丁

通过`补丁`为`st`添加额外的功能。

补丁下载地址：[https://st.suckless.org/patches/](https://st.suckless.org/patches/)

### 打补丁

---

一般情况下，补丁文件都会说明是基于哪个版本制作出来的补丁。

例：

`st-anysize`最新的补丁是基于`st-0.8.4`制作出来的补丁。

![st-anysize-0.8.4](images/st-anysize-0.8.4.png)

#### 使用`git`管理打补丁后的`st`。

---

在打补丁之前，可以创建一个指向该补丁版本的git分支。

```sh
# 创建版本指向0.8.4，分支命为st-anysize-0.8.4的git分支
git switch -c st-anysize-0.8.4 0.8.4
```


将补丁文件放在`~/patches`目录下，通过`patch`命令打补丁。

```sh
# 在"st-anysize-0.8.4"分支上打"st-anysize-0.8.4.diff"补丁。
patch < ~/patches/st-anysize-0.8.4.diff

# git提交修改
git commit -am "patch: st-anysize-0.8.4"
```

将`st-anysize-0.8.4`分支合并到`master`分支。

合并分支如果有冲突就解决冲突。

```sh
# 切换到"master"分支
git switch master

# 合并分支
git merge st-anysize-0.8.4
```

重新编译安装。

```sh
rm -rf config.h && sudo make clean install
```

打补丁前，屏幕右侧有空隙。

![st](./images/st.png)

打补丁后，`st`占满了屏幕。

![st-anysize](./images/st-anysize.png)

### 代码托管和官方代码同步

---

查看远程仓库地址

```sh
git remote -v
```

![origin-to-suckless](images/origin-to-suckless.png)

发现`origin`指向官方的仓库。

修改：将`upstream`指向官方的仓库，`origin`指向自己的仓库。

```sh
# 将"upstream"指向官方的仓库
git remote rename origin upstream

# 添加自己的仓库地址
git add remote origin <自己的仓库地址>
```

将配置好的`dwm`推送到自己的远程仓库。

```sh
# 推送所有的分支和tags
git push origin --all && git push origin --tags
```

官方代码同步。

```sh
git pull upstream master
```

如果`git pull`有冲突就解决冲突。

### 补丁推荐

---

```
终端透明：st-alpha-0.8.2.diff

终端占满屏幕：st-anysize-0.8.1.diff

输入时隐藏鼠标：st-hidecursor-0.8.1.diff

支持Fira Code字体：st-ligatures-alpha-scrollback-20200428-28ad288.diff
```
