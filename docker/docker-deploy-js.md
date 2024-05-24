# 使用 docker 部署 express 和 vue 项目

本文使用的镜像是基于 `alpine` 版本的镜像, 因为这个版本的镜像体积较小。

## 部署 express 项目

一个基本的 `express` 项目结构如下：

```tree
.
├── app.js
├── bin
├── Dockerfile
├── package.json
├── package-lock.json
├── public
├── routes
└── views
```

其中 `Dockerfile` 需要自己创建并添加以下内容：

```Dockerfile
# <version>-alpine以指定node的版本，如node:10-alpine
FROM node:alpine

# 设置工作目录
WORKDIR /usr/src/app

# 复制package.json 和 package-lock.json
COPY package*.json ./

# 安装依赖
RUN npm install

# 复制代码
COPY . .

# 指定端口
EXPOSE 3000

# 启动命令，这里写的是package.json中的启动命令
CMD ["npm", "start"]
```

构建镜像。

```sh
docker build -t my-express .
```

运行镜像。

```sh
docker run -d -p 3000:3000 my-express
```

:confetti_ball: 到这里 `express` 项目已经部署成功了。

## 部署 vue 项目

一个基本的 `vue` 项目结构如下：

```tree
.
├── default.conf
├── Dockerfile
├── index.html
├── jsconfig.json
├── package.json
├── package-lock.json
├── public
├── src
└── vite.config.js
```

其中 `Dockerfile` 和 `default.conf` 需要自己创建。

自定义 `default.conf` 的目的是为了解决使用 `nginx` 部署的 `vue` 项目，在不同的路由下刷新页面会导致 `404` 的问题，参考[Different History Modes](https://router.vuejs.org/guide/essentials/history-mode.html#nginx)。

`default.conf` 的内容如下：

```nginx
server {
  listen       80;
  listen  [::]:80;
  server_name  localhost;

  location / {
    root   /usr/share/nginx/html;
    index  index.html index.htm;
    try_files $uri $uri/ /index.html;
  }

  error_page   500 502 503 504  /50x.html;
  location = /50x.html {
    root   /usr/share/nginx/html;
  }
}
```

`Dockerfile` 的内容如下：

```Dockerfile
FROM node:alpine as builder

WORKDIR /build

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

FROM nginx:alpine

COPY default.conf /etc/nginx/conf.d/default.conf

COPY --from=builder /build/dist /usr/share/nginx/html
```

构建镜像。

```sh
docker build -t my-vue .
```

运行容器。

```sh
docker run -d -p 80:80 my-vue
```

:tada: 到这里 `vue` 项目已经部署成功了。

## 使用 docker-compose 编排多个容器

例如，这是一个 `express` 作为后端，`vue` 作为前端的项目：

```tree
.
├── backend
│   ├── app.js
│   ├── bin
│   ├── Dockerfile
│   ├── package.json
│   ├── package-lock.json
│   ├── public
│   ├── routes
│   └── views
├── frontend
│   ├── default.conf
│   ├── Dockerfile
│   ├── index.html
│   ├── jsconfig.json
│   ├── package.json
│   ├── package-lock.json
│   ├── public
│   ├── src
│   └── vite.config.js
└── compose.yaml
```

`compose.yaml` 的内容如下：

```yaml
# 指定docker-compose的版本
version: "2"

services:
  backend:
    build: ./backend
    container_name: project-backend
    ports:
      - "3000:3000"
    networks:
      - project

  frontend:
    build: ./frontend
    container_name: project-frontend
    ports:
      - "80:80"
    networks:
      - project

networks:
  project:
    name: project
    driver: bridge
```

启动服务。

```sh
docker-compose up -d
```

:v: 到这里，`express` 和 `vue` 都已经部署成功了。
