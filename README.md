# demo

#### 部署静态文件

```bash
$ docker run --name my-site -v /my_local_path/content:/usr/share/nginx/html:ro -d nginx
```

`/my_local_path/content` 存放你的 `.html` 文件。`/my_local_path`是一个绝对路径。

```
$ docker run --name my-site -v "$(pwd)"/content:/user/share/nginx/html:ro -d nginx
```

也可以用$(pwd)代替绝对路径。

#### 启动一个 bash

有时候你需要一个 ubuntu 的 bash，可以直接通过 docker 一次性启动一个。

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


