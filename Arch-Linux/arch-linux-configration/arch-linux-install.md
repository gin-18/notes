# Arch Linux 安装

[TOC]

## 安装准备

### 下载镜像

---

`Arch Linux`官方镜像下载地址：https://archlinux.org/download/

### 制作u盘启动器

---

#### Linux 下使用`dd`命令制作u盘启动器

---

```sh
# 确认u盘路径
sudo fdisk -l

# 取消挂载u盘
sudo umount <u盘路径>

# 格式化u盘
sudo mkfs.vfat -I <u盘路径>

# 使用dd命令
sudo dd if=<镜像文件路径> of=<u盘路径> status=progress
```

#### Window 下使用 Rufus 制作u盘启动器

---

使用`Rufus`制作u盘启动器的写入方式为`DD`。

### 官方安装向导

---

`Arch Linux`官方安装向导：https://wiki.archlinux.org/index.php/Installation_guide

## UEFI 下安装 Arch Linux

### 连接互联网

---

安装`Arch Linux`必须连通网络。

可以插入`网线`或使用`wifi`。

#### 连接 wifi

---

使用`iwd`连接`wifi`。

```sh
# 进入iwd交互界面
iwctl

# 查看设备名
device list

# 扫描网络
station <设备名> scan

# 查看网络名称
station <设备名> get-networks

# 连接网络
station <设备名> connect <网络名称>
```

### 更新系统时钟

---

```sh
timedatectl set-ntp true
```

### 磁盘分区

---

可以使用`fdisk`命令进行磁盘分区，也可以使用`cfdisk`命令进行磁盘分区。

`cfdisk`命令拥有交互界面。

```sh
cfdisk
```

<++>
