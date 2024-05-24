# Docker

[TOC]

## 安装 Docker

### Arch Linux

```sh
sudo pacman -S docker

# 启动Docker
sudo systemctl start docker
```

### Debian

更新 `apt` 并下载相应软件。

```sh
sudo apt update

sudo apt install \
   ca-certificates \
   curl \
   gnupg \
   lsb-release
```

添加 `Docker` 官方 `GPG key`。

```sh
sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

设置仓库。

```sh
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

安装 `Docker` 引擎。

```sh
sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

## 镜像加速

### 阿里云镜像加速

通过修改 `daemon` 配置文件 `/etc/docker/daemon.json` 来使用加速器。

```sh
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://i9w1wdva.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

## 以普通用户方式管理Docker

创建Docker组。

```sh
sudo groupadd docker
```

将用户添加到Docker组。

```sh
sudo usermod -aG docker $USER
```

激活组更新。

```sh
newgrp docker
```

验证是否能以普通用户运行Docker命令。

```sh
docker run hello-world
```

## 镜像

拉取镜像。

```sh
docker pull <image>:<tag>
```

查看镜像。

```sh
docker images
```

删除镜像。

```sh
docker rmi <image id>
```

镜像导入与导出。

```sh
# 导出
docker save -o <path/name.image> <image id>

# 导入
docker load -i <name.image>

# 改名
docker tag <image id> <name>:<tag>
```

## 容器

<++>

## Docker网络 - docker0

<++>

## 部署应用

### mongodb

```sh
docker run -d -p 27017:27017 --name my-mongodb \
-v ~/docker_volume/mongo/configdb:/data/configdb \
-v ~/docker_volume/mongo/db:/data/db \
-v ~/docker_volume/mongo/backup:/data/backup \
mongo --auth
```

### nginx

```sh
docker run -d -p 80:80 -p 443:443 --name my-nginx \
-v ~/docker_volume/nginx/html:/usr/share/nginx/html \
-v ~/docker_volume/nginx/conf.d:/etc/nginx/conf.d \
-v ~/docker_volume/nginx/nginx.conf:/etc/nginx/nginx.conf \
nginx
```

## Docker 运行 Linux，利用 VNC 实现 GUI 界面

### 运行 Arch Linux

运行容器。

```sh
sudo docker run -it -d -p 5901:5901 --name arch_vnc archlinux
```

进入容器。

```sh
sudo docker exec -it arch_vnc /bin/bash
```

修改 `pacman` 国内源。

```sh
# 添加国内源
echo \
'Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch
Server = http://mirrors.aliyun.com/archlinux/$repo/os/$arch
Server = https://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch' > /etc/pacman.d/mirrorlist

# 更新源
pacman -Syy
```

安装基础包。

```sh
# 基础包
pacman -S xorg make gcc git neovim

# 字体
pacman -S wqy-microhei ttf-fira-code
```

安装图形化界面。

```sh
# 克隆 dwm
git clone https://git.suckless.org/dwm

# 编译安装
cd dwm && make install
```

安装配置 `vncserver`。

```sh
# 安装 vncserver
pacman -S tigervnc

# 初始化密码
vncpasswd

# 配置
echo 'session=dwm' >> ~/.vnc/config
```

创建 `/usr/share/xsessions` 目录。

```sh
mkdir -p /usr/share/xsessions
```

添加 `dwm` 的 `desktop entry`，在 `/usr/share/xsessions/dwm.desktop` 文件中添加以下内容：

```sh
[Desktop Entry]
Encoding=UTF-8
Name=Dwm
Comment=Dynamic window manager
Exec=dwm
Icon=dwm
Type=Xsession
```

启动 `vncserver`。

```sh
# ":1"会在5900端口上+1
vncserver :1

# 在容器外可以使用以下命令
sudo docker exec -u root -d arch_vnc bash -c '/usr/sbin/vncserver :1'
```




