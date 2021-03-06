# Docker笔记

---

## Docker卸载和安装

Docker安装的前提条件：

* Docker运作在CentOS 7上，要求系统为64位，系统内核版本为3.10以上
* Docker运作在CentOS 6.5或更高版本，要求系统为64位，系统内核版本为2.6.32-431或更高版本

查看自己Linux的内核：uname -r

### 在CentOS上安装Docker

卸载旧版本Docker

```shell
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

使用Docker仓库安装

1.设置Docker仓库

```shell
sudo yum install -y yum-utils
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

2.安装最新版的Docker引擎和容器

```shell
sudo yum install docker-ce docker-ce-cli containerd.io
```

3.启动Docker

```shell
sudo systemctl start docker
```

4.通过运行hello-world镜像验证Docker是否成功安装

```shell
sudo docker run hello-world
```

卸载Docker

1.卸载Docker引擎，CLI和容量包

```shell
sudo yum remove docker-ce docker-ce-cli containerd.io
```

2.主机上的图像、容器、卷或自定义配置文件不会自动删除，删除所有图像、容器和卷

```shell
sudo rm -rf /var/lib/docker
```

---

## Docker安装后配置

### 以普通用户方式管理Docker

1.创建Docker组

```shell
sudo groupadd docker
```

2.将用户添加到Docker组

```shell
sudo usermod -aG docker $USER
```

3.激活组更新

```shell
newgrp docker
```

4.验证是否能以普通用户运行Docker命令

```shell
docker run hello-world
```

---

## 镜像加速

### 阿里云镜像加速

**CentOS配置镜像加速**

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

---

