---
title: Docker常用命令
date: 2023-08-16 18:15:46
tags: Docker
---

## 镜像

**查看镜像：**

```
docker images
```

**拉取镜像：**

```bash
docker pull 镜像名称:tag
```

**搜索镜像：**

```bash
docker search 镜像名称
```

**删除镜像：**

```bash
docker rmi 镜像id ｜ 镜像名称
```

**构建镜像：**

```
docker build -t demo  . 
```

> 最后有个 . 表示上下文路径
>
> build工作由Dokcer引擎完成，所以要给Docker引擎提供上下文环境。构建镜像时，客户端会将路径下的所有内容打包，并上传给 Docker 引擎，这样它就可以获取构建镜像所需的一切文件了。

`-t`:命名为demo

​	

## 容器

**查看正在运行的容器：**

```
docker ps
```

`a`:查看所有容器

**创建启动容器:**

```shell
	docker run IMAGE:TAG
```

`IMAGE`: 镜像名称
`TAG`: 标签，镜像版本号

- `-t`: 让 Docker 分配一个伪终端（pseudo-tty）并绑定到容器的标准输入上
- `-i`: 让容器的标准输入保持打开
- `-d` 参数可以让容器以后台的方式运行
- `--name`：为创建的容器命名
- `-p`：表示端口映射，前者是宿主机端口，后者是容器内的映射端口。可以使用多个 -p 做多个端口映射
- `-v`：目录映射关系

**以交互的方式运行容器：**

```go
docker run -t -i ubuntu:latest /bin/bash
```

**停止与启动容器：**

```bash
# 停止容器
docker stop 容器名称|容器ID
# 启动容器
docker start 容器名称|容器ID
```

**查看容器元信息：**

```bash
docker inspect 容器名称|容器ID
```

**删除容器：**

```
docker rm 容器名称|容器ID
```

**进入正在运行的容器：**

```
  docker exec -it 容器名称|容器ID /bin/bash 
```



## 数据卷

**挂载数据卷：**

```bash
使用-v参数，格式为宿主机目录:容器目录，例如：
docker run -v /mszlu/docker/centos/data:/usr/local/data centos:7
```

**查看 volume 数据卷信息：**

```bash
docker volume ls
```

**匿名挂载：**

```bash
只用写容器目录
宿主机对应的目录会在 /var/lib/docker/volumes 中生成
```

**查看当前容器挂载情况：**

```bash
通过查看容器元信息查看
docker inspect centos7-02（容器名称）
```

