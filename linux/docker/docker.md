# Docker

## 安装

```
sudo pacman -S docker
```

启动Docker

```shell
sudo systemctl start docker
```

## 镜像加速

#### 阿里云镜像加速

通过修改daemon配置文件/etc/docker/daemon.json来使用加速器

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

创建Docker组

```shell
sudo groupadd docker
```

将用户添加到Docker组

```shell
sudo usermod -aG docker $USER
```

激活组更新

```shell
newgrp docker
```

验证是否能以普通用户运行Docker命令

```shell
docker run hello-world
```

## Docker网络(docker0)

<++>

## 镜像

拉取镜像

```shell
docker pull <image>:<tag>
```

查看镜像

```shell
docker images
```

删除镜像

```shell
docker rmi <image id>
```

镜像导入与导出

```shell
# 导出
docker save -o <path/name.image> <image id>

# 导入
docker load -i <name.image>

# 改名
docker tag <image id> <name>:<tag>
```

## 容器

<++>










