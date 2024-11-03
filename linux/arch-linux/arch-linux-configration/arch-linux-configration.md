# Arch Linux 配置

## 添加 `archlinuxcn` 源

清华大学开源软件镜像站：[ArchlinuxCN镜像使用帮助](https://mirrors.tuna.tsinghua.edu.cn/help/archlinuxcn/)

在 `/etc/pacman.conf` 文件中添加以下代码：

```
[archlinuxcn]
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
```

安装 `archlinuxcn-keyring` 包导入 `GPG key` 。

```sh
sudo pacman -S archlinuxcn-keyring
```

## 显卡驱动

查看显卡和显卡驱动。

```sh
lspci -k | grep -A 2 -E "(VGA|3D)"
```

安装 `nvidia` 驱动。

```sh
sudo pacman -S nvidia
```

## git

安装git。

```sh
sudo pacman -S git
```

添加用户名和邮件。

```sh
git config --global user.name <your name>

git config --global user.email <email@example.com>
```

修改 `/etc/hosts` 文件，添加以下内容：

```sh
# Github Hosts
# domain: github.com
140.82.113.4 github.com
140.82.114.9 nodeload.github.com
140.82.112.5 api.github.com
140.82.112.10 codeload.github.com
185.199.108.133 raw.github.com
185.199.108.153 training.github.com
185.199.108.153 assets-cdn.github.com
185.199.108.153 documentcloud.github.com
140.82.114.17 help.github.com

# domain: githubstatus.com
185.199.108.153 githubstatus.com

# domain: fastly.net
199.232.69.194 github.global.ssl.fastly.net

# domain: githubusercontent.com
185.199.108.133 raw.githubusercontent.com
185.199.108.154 pkg-containers.githubusercontent.com
185.199.108.133 cloud.githubusercontent.com
185.199.108.133 gist.githubusercontent.com
185.199.108.133 marketplace-screenshots.githubusercontent.com
185.199.108.133 repository-images.githubusercontent.com
185.199.108.133 user-images.githubusercontent.com
185.199.108.133 desktop.githubusercontent.com
185.199.108.133 avatars.githubusercontent.com
185.199.108.133 avatars0.githubusercontent.com
185.199.108.133 avatars1.githubusercontent.com
185.199.108.133 avatars2.githubusercontent.com
185.199.108.133 avatars3.githubusercontent.com
185.199.108.133 avatars4.githubusercontent.com
185.199.108.133 avatars5.githubusercontent.com
185.199.108.133 avatars6.githubusercontent.com
185.199.108.133 avatars7.githubusercontent.com
185.199.108.133 avatars8.githubusercontent.com
# End of the section
```

## zsh & zinit

GitHub：[zinit](https://github.com/zdharma-continuum/zinit)

安装 `zsh` 并切换到 `zsh`。

```sh
sudo pacman -S zsh;chsh -s /bin/zsh
```

安装 `zinit`。

```sh
ZINIT_HOME="${XDG_DATA_HOME:-${HOME}/.local/share}/zinit/zinit.git"

mkdir -p "$(dirname $ZINIT_HOME)"

git clone https://github.com/zdharma-continuum/zinit.git "$ZINIT_HOME"
```

## fcitx5 输入法

ArchWiki：[fcitx5](https://wiki.archlinux.org/title/Fcitx5)

安装相应的软件包。

```sh
sudo pacman -S fcitx5-im fcitx5-chinese-addons fcitx5-nord

或

sudo pacman -S fcitx5 fcitx5-chinese-addons fcitx5-qt fcitx5-gtk fcitx5-configtool fcitx5-nord
```

设置环境变量，在 `~/.pam_environment` 添加以下代码：

```sh
GTK_IM_MODULE DEFAULT=fcitx
QT_IM_MODULE  DEFAULT=fcitx
XMODIFIERS    DEFAULT=\@im=fcitx
INPUT_METHOD  DEFAULT=fcitx
SDL_IM_MODULE DEFAULT=fcitx
```

## 声音和蓝牙

安装相应的软件包，其中：

- `alsa-utils` 软件包提供声音。

- `bluez` 软件包提供蓝牙的协议栈。

- `bluez-utils` 软件包提供 `bluetoothctl` 工具。

```sh
sudo pacman -S bluez bluez-utils alsa-utils pulseaudio pulseaudio-alsa pulseaudio-bluetooth
```

启动蓝牙和 `pulseaudio` 服务。

```sh
sudo systemctl start bluetooth

sudo systemctl enable bluetooth

# 确保没有pulseaudio启动
pulseaudio -k

# 启动pulseaudio服务
pulseaudio --start
```

使用 `bluetoothctl` 工具连接蓝牙。

```sh
# 启动bluetoothctl交互命令
bluetoothctl

# 打开代理(官方推荐)
agent on

agent KeyboardOnly

default-agent

# 打开控制器电源，默认关闭
power on

# 获取设备的MAC地址
devices

# 搜索所有可配对的设备
scan on

# 配对设备
pair MAC_address

# 连接设备
connent MAC_address
```

## 双系统grub添加Windows 10引导启动项

如果 `grub` 引导界面没有 `Windows 10` 启动项，则需要手动添加。

查看 `Win10` 的 `EFI` 启动项在磁盘的哪个分区。

```sh
fdisk -l
```

输出结果中 `Size Type` 表示分区类型，显示 `EFI` 的就是引导分区，找到 `Windows 10` 的引导分区的设备号。

查看分区的 `uuid`，使用 `blkid` 命令或 `grub` 命令均可。

```sh
blkid /dev/nvme0n1p1

或者

grub-probe -t fs_uuid -d /dev/nvme0n1p1
```

在 `/boot/grub/grub.cfg` 的 `30_osprobe` 文件中添加以下代码(其中 `<uuid>` 填写 `Windows 10` 的引导分区的 `uuid`)：

```
menuentry 'Microsoft Windows 10' --class windows {
    insmod part_gpt
    insmod fat
    insmod chain
    search --fs-uuid --no-floppy --set=root <uuid>
    chainloader (${root})/EFI/Microsoft/Boot/bootmgfw.efi
}
```

## 虚拟机

### virtualbox

ArchWiki：[VirtualBox](https://wiki.archlinux.org/title/VirtualBox)

安装 `virtualbox` 软件包和内核模块 `virtualbox-host-modules-arch`。

如果使用其他内核，需要安装的是 `virtualbox-host-dkms`。

```sh
sudo pacman -S virtualbox virtualbox-host-modules-arch
```

在 `VirtualBox` 所使用的内核模块中，只有 `vboxdrv` 是必须的，该模块必须在虚拟机运行之前加载。

```sh
modprobe vboxdrv
```

建议使用高级功能时将一下模块都加载。

```sh
modprobe vboxnetadp vboxnetflt vboxpci
```

#### virtualbox下安装macOS

在启动VM之前，虚拟机目录运行以下命令：

```sh
VBoxManage modifyvm "MyMacVM" --cpuid-set 00000001 000106e5 00100800 0098e3fd bfebfbff

VBoxManage setextradata "MyMacVM" "VBoxInternal/Devices/efi/0/Config/DmiSystemProduct" "iMac11,3"

VBoxManage setextradata "MyMacVM" "VBoxInternal/Devices/efi/0/Config/DmiSystemVersion" "1.0"

VBoxManage setextradata "MyMacVM" "VBoxInternal/Devices/efi/0/Config/DmiBoardProduct" "Iloveapple"

VBoxManage setextradata "MyMacVM" "VBoxInternal/Devices/smc/0/Config/DeviceKey" "ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc"

VBoxManage setextradata "MyMacVM" "VBoxInternal/Devices/smc/0/Config/GetKeyFromRealSMC" 1

VBoxManage setextradata "MyMacVM" VBoxInternal2/EfiGopMode 4
```

### VMwarw Workstation

`vmware workstation 16 pro` 序列号

```
ZF3R0-FHED2-M80TY-8QYGC-NPKYF
```

## 亮度调整

使用`xorg-xbacklight`来调整屏幕的亮度，`xbacklight`命令默认只对`Intel`核显有效。

调整屏幕亮度就是在硬件层面调整LED灯的功率，在linux中通过acpi(高级配置与电源接口)来控制。其他核显可以安装acpi的亮度控制取代`xbacklight`的功能。

```sh
sudo pacman -S acpilight
```

将当前用户添加到`video`组，实现免`root`控制亮度。

```sh
sudo gpasswd video -a <username>
```

`acpilight`兼容`xbacklight`，重启之后就可以通过以下命令控制亮度：

```sh
# 获取当前亮度
xbacklight -get

# 设置亮度
xbacklight -set <number>

# 增加亮度
xbacklight -inc <number>

# 降低亮度
xbacklight -dec <number>
```

## grub2-themes

GitHub：[grub2-themes](https://github.com/vinceliuice/grub2-themes)

克隆仓库。

```sh
git clone https://github.com/vinceliuice/grub2-themes.git && cd grub2-themes
```

安装。

```sh
sudo ./install.sh -t vimix -s 4k
```

重新生成`grub`配置文件。

```sh
grub-mkconfig -o /boot/grub/grub.cfg
```

### grub.cfg

```
menuentry "System shutdown" --class shutdown {
    echo "System shutting down..."
    halt
}

menuentry "System restart" --class restart {
    echo "System rebooting..."
    reboot
}

menuentry 'UEFI Firmware Settings' $menuentry_id_option 'uefi-firmware' --class find.efi {
    fwsetup
}
```

## uxplay(ios投屏工具)

安装uxplay。

```sh
yay -S uxplay-git
```

启动服务。

```sh
sudo systemctl start avahi-daemon.service
```

## 美化

[Arch Linux 美化](./arch-linux-beautify.md)
