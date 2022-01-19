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

编译安装后，会产生`config.h`文件。

通过`config.h`文件配置`st`。

## 5. st补丁

通过`补丁`为`st`添加额外的功能。

补丁下载地址：[https://st.suckless.org/patches/](https://st.suckless.org/patches/)

### 打补丁

---

将补丁文件放在`st`目录下。通过`patch`命令打补丁。

如果打补丁失败，需要手动添加。

例：

打一个`st占满屏幕`的补丁。

```sh
patch < st-anysize-0.8.1.diff
```

打补丁前，屏幕右侧有空隙。

![st](./images/st.png)

打补丁后，`st`占满了屏幕。

![st-anysize](./images/st-anysize.png)

### 补丁推荐

---

```
终端透明：st-alpha-0.8.2.diff

终端占满屏幕：st-anysize-0.8.1.diff

输入时隐藏鼠标：st-hidecursor-0.8.1.diff

支持Fira Code字体：st-ligatures-alpha-scrollback-20200428-28ad288.diff
```
