## demo

#### 部署静态文件

```bash
$ docker run --name my-site -v /my_local_path/content:/usr/share/nginx/html:ro -d nginx
```

`/my_local_path/content` 存放你的 `.html` 文件。`/my_local_path`是一个绝对路径。

```
$ docker run --name my-site -v "$(pwd)"/content:/usr/share/nginx/html:ro -d nginx
```

也可以用$(pwd)代替绝对路径。

#### ubuntu bash

临时需要一个 ubuntu 的 bash。

```
$ docker run -it ubuntu bash
```
#### 做一个代理 nginx

先创建一个 `location`。命名为: `your_site.conf`。

并放在你本地自己新建的`conf.d` 文件夹

```
server {
  listen  80;
  # listen on the www host
  server_name  xx.yyy.com;

  location / {
    # proxy to your service
     proxy_pass  http://192.168.1.8:3000;
  }
}
```

运行 nginx 容器并将本地的`conf.d`文件夹挂在到容器内。

```
$ docker run --name my-site -v "$(pwd)"/conf.d:/etc/nginx/conf.d -p 80:80 -d nginx
```

#### node bash

```
$ docker run -it node bash
```

#### 用 docker 运行一个 node 项目

```
FROM node
ADD ./ /opt/app/
WORKDIR /opt/app
CMD ["node", "index.js"]
```

```
$ docker build .
$ docker run <image_id>
```

https://github.com/xugy0926/docker-sample/tree/master/demo/node_project

#### mongodb

```
docker run -d -p 27017:27017 -p 28017:28017 -e AUTH=no tutum/mongodb
```

## docker 基本操作

#### 进入到容器

```bash
$ sudo docker exec -it <docker-id or docker-name> /bin/bash 
```

#### 从容器中拷贝文件到宿主机

```bash
$ docker cp contaienr-name:/folder/file ./
```

#### 从宿主机拷贝文件到容器

```bash
$ docker cp ./file container-name:/folder
```


