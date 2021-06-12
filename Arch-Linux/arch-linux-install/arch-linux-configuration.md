# 安装完成Arch Linux后的配置

## 需要安装的软件

```
1. base-devel
2. xorg-server
3. xorg-xinit
4. xorg-xrandr
5. i3-gaps
6. alacritty
7. ranger
8. fzf
9. openssh
10. git
11. python3
12. python-pip
13. nodejs
14. yarn
15. npm
16. simplescreenrecorder
17. screenkey
18. flameshot
19. gpick
20. ffmpegthumbnailer
21. zathura
22. zathura-pdf-poppler
23. fcitx5
24. fcitx5-chinese-addons
25. fcitx5-qt
26. fcitx5-gtk
27. fcitx5-configtool
28. ctags
29. fd
30. bat
31. alsa-utils
32. pulseaudio
33. pulseaudio-alsa
34. pulseaudio-bluetooth
35. bluez-utils
36. nvidia
37. virtualbox
38. virtualbox-host-modelus-arch
39. tlp
40. xf86-video-intel
41. neovim-remote
42. lxappearance
43. materia-gtk-theme
44. papirus-icon-theme
45. xorg-xbacklight
46. betterlockscreen
47. xclip
48. xorg-xsetroot
49. duf
50. acpi
51. retroarch
52. retroarch-assets-xmb
53. retroarch-assets-ozone
54. nordic-darker-theme
55. nordic-theme
56. the_silver_searcher
57. escrotum-git
58. peek
59. qt5ct
60. xsettingsd
61. qt5-styleplugins
62. gthumb
63. xfce4-power-manager
```

### nvidia显卡驱动

查看显卡和显卡驱动

```
lspci -k | grep -A 2 -E "(VGA|3D)"
```

安装nvidia驱动

```
sudo pacman -S nvidia
```

### 双系统grub添加Windows10引导启动项

如果grub引导界面没有Win10启动项，则需要手动添加

#### 查看Win10的EFI启动项在磁盘的哪个分区

```
fdisk -l
```

![fdisk-l](./screenshot/fdisk-l.png)

输出结果中"Size Type"表示分区类型，显示EFI的就是引导分区，找到Win10的引导分区的设备号

#### 查看分区的"uuid"，使用"blkid"命令或"grub"命令均可

```
blkid /dev/nvme0n1p1<设备号>

或者

grub-probe -t fs_uuid -d /dev/nvme0n1p1<设备号>
```

#### 在/boot/grub/grub.cfg的30_osprobe文件中添加以下代码

```
menuentry 'Microsoft Windows 10' {
  insmod part_gpt
	insmod fat
	insmod chain
	search --fs-uuid --no-floppy --set=root xxxx-xxxx
	chainloader (${root})/EFI/Microsoft/Boot/bootmgfw.efi
}
```

其中"xxxx-xxxx"是分区的"uuid"

### ssh服务

安装"openssh"软件包

```
pacman -S openssh
```

启动ssh服务

```
systemctl start sshd

systemctl enable sshd
```

### 添加普通用户

安装"base-devel"软件包

```
pacman -S base-devel
```

添加新普通用户

```
useradd -mG wheel gin
```

给普通用户添加密码

```
passwd gin
```

修改/etc/sudoers文件

```
将%wheel ALL=(ALL) ALL的注释放开
```

### 字体

暂安装以下字体

```
1. ttf-symbola
2. adobe-source-code-pro
4. nerd-fonts-complete
5. wqy-zenhei 
6. ttf-inconsolata 
7. ttf-dejavu 
8. ttf-nerd-fonts-symbols-mono
9. otf-font-awesome
```

查看以安装的字体

```
fc-list
```

### i3wm

安装"i3-gaps"软件包

```
sudo pacman -S i3-gaps
```

#### 使用startx启动i3wm

在家目录中创建.xinitrc文件

```
nvim .xinitrc

添加：exec i3
```

#### 启动i3

```
startx
```

#### 自动启动X

将以下脚本写入/etc/profile文件中，登录后就可以自动启动startx

```
if [ -z "${DISPLAY}" ] && [ "${XDG_VTNR}" -eq 1 ]; then
	exec startx
fi
```

也可以将以上内容单独写成一个脚本文件放在/etc/profile.d目录中，登录时会读取该目录下的脚本文件


### alacritty

安装"alacritty"软件包

```
sudo pacman -S alacritty
```

alacritty的配置文件是~/.config/alacritty/alacritty.yml

### 虚拟机

---

#### virtualbox

安装"virtualbox"软件包和内核模块"virtualbox-host-modelus-arch"

如果使用其他内核，需要安装的是"virtualbox-host-dkms"

在"VirtualBox"所使用的内核模块中，只有"vboxdrv"是必须的，该模块必须在虚拟机运行之前加载

```
modprobe vboxdrv
```

建议使用高级功能时将一下模块都加载

```
modprobe vboxnetadp vboxnetflt vboxpci
```

virtualbox下安装macOS

在启动VM之前，虚拟机目录运行以下命令

```
1. VBoxManage modifyvm "MyMacVM" --cpuid-set 00000001 000106e5 00100800 0098e3fd bfebfbff
2. VBoxManage setextradata "MyMacVM" "VBoxInternal/Devices/efi/0/Config/DmiSystemProduct" "iMac11,3"
3. VBoxManage setextradata "MyMacVM" "VBoxInternal/Devices/efi/0/Config/DmiSystemVersion" "1.0"
4. VBoxManage setextradata "MyMacVM" "VBoxInternal/Devices/efi/0/Config/DmiBoardProduct" "Iloveapple"
5. VBoxManage setextradata "MyMacVM" "VBoxInternal/Devices/smc/0/Config/DeviceKey" "ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc"
6. VBoxManage setextradata "MyMacVM" "VBoxInternal/Devices/smc/0/Config/GetKeyFromRealSMC" 1
7. VBoxManage setextradata "MyMacVM" VBoxInternal2/EfiGopMode 4
```

#### VMwarw Workstation

vmware workstation 16 pro序列号

```
ZF3R0-FHED2-M80TY-8QYGC-NPKYF
```

### 蓝牙配置

---

#### 确保相应的软件包存在

```
1. bluez
2. bluez-utils
3. alsa-utils
4. pulseaudio
5. pulseaudio-alsa
6. pulseaudio-bluetooth
```

bluez，这个软件包提供蓝牙的协议栈

bluez-utils，这个软件包提供"bluetoothctl"工具

#### 启动蓝牙和pulseaudio服务

```
systemctl start bluetooth

systemctl enable bluetooth

# 确保没有pulseaudio启动
pulseaudio -k

# 启动pulseaudio服务
pulseaudio --start
```

#### 使用bluetoothctl工具连接蓝牙

```shell
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

### 亮度调整

使用"xorg-xbacklight"来调整屏幕的亮度

"xbacklight"命令默认只对Intel核显有效

调整屏幕亮度就是在硬件层面调整LED灯的功率，在linux中通过acpi(高级配置与电源接口)来控制。其他核显可以安装acpi的亮度控制取代"xbacklight"的功能

```
sudo pacman -S acpilight
```

将当前用户添加到"video"组，实现免"root"控制亮度

```
sudo gpasswd video -a <username>
```

"acpilight"兼容"xbacklight"，重启之后就可以通过以下命令控制亮度

```
# 获取当前亮度
xbacklight -get

# 设置亮度
xbacklight -set <number>

# 增加亮度
xbacklight -inc <number>

# 降低亮度
xbacklight -dec <number>
```

### uxplay(ios投屏工具)

---

安装uxplay

```
yay -S uxplay-git
```

启动服务

```
sudo systemctl start avahi-daemon.service
```

<++>

