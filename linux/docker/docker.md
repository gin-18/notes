# Docker

---

[TOC]

## 安装 Docker

---

### Arch Linux

---

```
sudo pacman -S docker

# 启动Docker
sudo systemctl start docker
```

### Debian

---

更新 `apt` 并下载相应软件。

```shell
sudo apt update

sudo apt install \
   ca-certificates \
   curl \
   gnupg \
   lsb-release
```

添加 `Docker` 官方 `GPG key`。

```shell
sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

设置仓库。

```shell
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

安装 `Docker` 引擎。

```shell
sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

## 镜像加速

---

### 阿里云镜像加速

---

通过修改 `daemon` 配置文件 `/etc/docker/daemon.json` 来使用加速器。

```shell
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

---

创建Docker组。

```shell
sudo groupadd docker
```

将用户添加到Docker组。

```shell
sudo usermod -aG docker $USER
```

激活组更新。

```shell
newgrp docker
```

验证是否能以普通用户运行Docker命令。

```shell
docker run hello-world
```

## 镜像

---

拉取镜像。

```shell
docker pull <image>:<tag>
```

查看镜像。

```shell
docker images
```

删除镜像。

```shell
docker rmi <image id>
```

镜像导入与导出。

```shell
# 导出
docker save -o <path/name.image> <image id>

# 导入
docker load -i <name.image>

# 改名
docker tag <image id> <name>:<tag>
```

## 容器

---

<++>

## Docker网络(docker0)

---

<++>

## 部署应用

---

### mongodb

---

```sh
sudo docker run -d -p 27017:27017 -v ~/docker_volume/mongo/configdb:/data/configdb -v ~/docker_volume/mongo/db:/data/db mongo
```









