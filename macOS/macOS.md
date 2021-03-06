# macOS

## 官方镜像

官方地址 : https://support.apple.com/zh_CN/downloads/macos

## VMware安装macOS High Sierra

**准备的工具**

```
unlocker： https://github.com/paolo-projects/unlocker/releases

工具包：com.vmware.fusion.zip.tar
```

unlocker工具需要python3环境

**配置工具**

将com.vmware.fusion.zip.tar移动到uncloker的tools目录中或者将"darwin.iso

注视掉自动下载：有gettools.py的那一行

![autoload](./macOS.assets/20200417014900339.png)

以管理员身份运行unlocker中的win-install.cmd文件

**如果开机遇到问题或卡在开机界面不断重启** 

打开虚拟机安装的目录找到.vmx文件添加以下代码：

```
smc.version = "0"

// 最后一行添加
cpuid.1.eax = "00000000000000010000011010100101"
```

### 安装VMware tools

需要工具：darwin.iso

darwin.iso文件在com.vmware.fusion.zip.tar文件有：com.vmware.fusion.zip.tar\com.vmware.fusion.zip\payload\VMwareFusion.app\Contents\Library\isoimages

在虚拟机中加载镜像

## homebrewCN

homebrewCN的gitee的地址：https://gitee.com/cunkai/HomebrewCN

## Mac安装Windows10

## 下载镜像

微软官方: https://www.microsoft.com/zh-cn/software-download/windows10ISO

我告诉你: https://msdn.itellyou.cn/

## 安装windows的条件

磁盘够容量

cpu : Intel

## 不需要u盘的条件

cpu : intel

使用OS X EI Capitan或更高版本



## 使用"启动转换"

只有在搭载Intel处理器的Mac上才能使用"启动转换"

## 查看cpu,OS,OS版本和磁盘空间

**cpu**

在"关于本机"会显示一个标有"芯片"的项目并跟着这个芯片的名称


在搭载Intel处理器的Mac上，"关于本机"会显示一个标有"处理器"的项目并跟有Intel处理器的名称。搭载Intel处理器的Mac也称为基于Intel的Mac

**os和版本**

在"关于本机"中可以看到macOS的名称(例如：macOS Big Sur)，后面则是版本号


**磁盘空间**

在"关于本机" > 存储空间中查看磁盘空间,至少需要40G 

## 检查安全启动

确保在安装Windows之前"安全启动"的设置为"完整安全性"

在启动时,看见Apple标志后立即按住Command-R键. Mac会从macOS恢复功能启动

## 无需u盘安装

Boot Camp会在直接在磁盘分配一个8G的分区来存储windows10的安装文件以及驱动程序

系统安装完成之后会自动合并8G分区

在windows10安装过程中必须把系统安装到bootcamp分区

1. 下载镜像

2. 打开Boot Camp


3. 选择镜像和分区


分区确定后无法调整

分区后,点击安装

4. 安装驱动

打开我的电脑 > u盘 > BootCamp目录 > Setup程序

## u盘安装

1. 下载镜像

2. 先插入u盘

3. 打开Boot Camp


3.2 制作windows的安装u盘


选择镜像文件,点击继续(会删除u盘的所以文件)

5. 创建windows分区


重启之后会进入windows的安装界面

u盘安装在windows的安装界面需要选择备注为bootcamp的磁盘,将其进行格式化


6. 安装驱动

打开我的电脑 > BootCamp目录 > Setup程序

7. 解决u盘安装存储空间不足的情况


使用2015版win10镜像

---

默认启动Mac系统

系统偏好设置 > 启动磁盘

Boot Camp控制面板

开机选择系统

开机按下option键

## 虚拟机

parallels(要钱) : https://www.parallels.cn/

virtualbox : https://www.virtualbox.org/wiki/Downloads

## windows的安装

选择自定义安装

购买链接 : https://www.microsoft.com/zh-cn/windows/get-windows-10
