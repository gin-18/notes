# Arch Linux

Arch Linux官方安装向导：https://wiki.archlinux.org/index.php/Installation_guide

## 下载镜像

官方网址：https://archlinux.org/download/

## 安装

### 验证启动方式

---

```
ls /sys/firmware/efi/efivars
```

如果命令没有报错，则使用的是UEFI;如果目录不存在则可能使用的是BIOS。

### 连接互联网

---

插入网线或使用wifi。

#### 连接wifi

使用"iwd"连接wifi

```
# 进入iwd交互界面
iwctl

# 查看设备名
device list

# 扫描网络
station <设备名> sacn

# 查看网络名称
station <设备名> get-networks

# 连接网络
station <设备名> connent <网络名称>
```

如果使用的是虚拟机，则不需要进行这一步操作。

### 更新系统时钟

---

```
timedatectl set-ntp true
```

### 磁盘分区

---

#### BIOS磁盘分区

BIOS只需要分2个区。

| 挂载点 | 分区类型             |
|--------|----------------------|
| swap   | Linux swap(交换分区) |
| /mnt   | Linux                |

#### UEFI磁盘分区

UEFI需要创建3个分区：boot分区(启动分区)，swap分区，系统分区。

| 挂载点    | 分区类型             |
|-----------|----------------------|
| /mnt/boot | EFI系统分区          |
| swap      | Linux swap(交换分区) |
| /mnt      | Linux                |

可以使用fdisk命令进行磁盘分区，也可以使用cfdisk命令进行磁盘分区。

cfdisk命令拥有交互界面。

### 磁盘格式化

格式化boot分区

```
mkfs.fat -F32 /dev/sda1
```

格式化系统分区

```
mkfs.ext4 /dev/sda3
```

格式化swap分区

```
mkswap /dev/sda2
```

启动swap分区

```
swapon /dev/sda2
```

### 挂载

将系统分区/dev/sda3挂载到/mnt目录

```
mount /dev/sda3 /mnt
```

创建boot分区的挂载点

```
mkdir /mnt/boot
```

将boot分区/dev/sda1挂载到/mnt/boot目录

```
mount /dev/sda1 /mnt/boot
```

### 修改镜像列表

将中国的源放置到最前面

```
vim /etc/pacman.d/mirrorlist
```

### 安装系统

```
pacstrap /mnt base linux linux-firmware
```

等待系统安装完成

### 配置系统

```
genfstab -U /mnt >> /mnt/etc/fstab
```

### 进入系统

```
arch-chroot /mnt
```

界面发生变化说明已经进入系统

### 修改时区

```
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

### 同步系统时间

```
hwclock --systohc
```

### 本地化设置

进入系统没有编辑器，下载需要的编辑器

```
pacman -S neovim
```

修改/etc/locale.gen文件，去掉en_US.UTF-8 UTF-8的注释

```
nvim /etc/locale.gen
```

再执行locale-gen

```
locale-gen
```

创建/etc/locale.conf文件，在/etc/locale.conf文件中添加LANG=en_US.UTF-8

```
nvim /etc/locale.conf

添加
LANG=en_US.UTF-8
```

### 网络配置

创建/etc/hostname文件，在文件中添加自己的主机名

```
nvim /etc/hostname

添加自己的主机名
```

添加hosts，在/etc/hosts中添加以下内容：

```
127.0.0.1     localhost

::1           localhost

127.0.1.1     主机名.localdomain 主机名
```

### 给root用户添加密码

```
passwd
```

### 安装grub引导

安装"grub"和"efibootmgr"

```
pacman -S grub efibootmgr
```

双系统额外安装"intel-ucode"和"os-prober"

```
sudo pacman -S grub efibootmgr intel-ucode os-prober
```

<++>

创建/boot/grub目录

```
mkdir /boot/grub
```

生成grub的配置文件

```
grub-mkconfig > /boot/grub/grub.cfg
```

安装grub

```
grub-install --target=x86_64-efi --efi-directory=/boot
```

### 安装dhcpcd

dhcpcd用于新系统上网

```
pacman -S dhcpcd
```

### 退出系统

```
exit
```

### 取消挂载

```
umount -R /mnt
```

### 重启电脑

```
reboot
```

## 联网设置

启动dhcpcd

```
systemctl start dhcpcd

systemctl enable dhcpcd
```

### wifi连接

安装iwd软件包

```
pacman -S iwd

# 启动iwd
systemctl start iwd

systemctl enable iwd
```

iwd交互命令

```
# 进入iwd交互界面
iwctl

# 查看设备
device list

# 扫描网络
station <设备名> sacn

# 查看网络名称
station <设备名> get-networks

# 连接网络
station <设备名> connent <网络名称>
```
