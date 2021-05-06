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











