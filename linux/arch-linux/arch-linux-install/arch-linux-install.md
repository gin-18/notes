# Arch Linux 安装

## 安装准备

### 下载镜像

`Arch Linux` 官方镜像下载地址：https://archlinux.org/download/

### 制作u盘启动器

#### Linux 下使用 dd 命令制作u盘启动器

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

使用 `Rufus` 制作u盘启动器的写入方式为 `DD`。

### 官方安装向导

`Arch Linux` 官方安装向导：https://wiki.archlinux.org/index.php/Installation_guide

## UEFI 下安装 Arch Linux

[UEFI 下安装 Arch Linux](./uefi/arch-linux-install-uefi.md)

## BIOS 下安装 Arch Linux

[BIOS 下安装 Arch Linux](./bios/arch-linux-install-bios.md)
