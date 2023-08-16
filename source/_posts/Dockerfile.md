---
title: Dockerfile
---

# Dockerfile

## 常用指令

###### FROM

From指定基础镜像

```dockerfile
FROM golang:1.20.6 as build
```

as 起别名，下文可以使用

分阶段构建镜像可以大大减小镜像



###### COPY

COPY 源路径1... 目标路径

复制指令，支持从上下文目录中复制文件或文件夹到容器里的指定路径

> 当源路径为文件夹，复制的时候不是直接复制该文件夹，而是将文件夹中的内容复制到目标路径。
>
> 如果你想要复制整个文件夹，包括文件夹本身，你可以在源路径后面添加一个 `/`
>
> 目标路径不需要提前创建好，路径不存在会自动创建。目标路径可以是容器内的绝对路径，也可以是相对于工作目录的相对路径（工作目录可以用 `WORKDIR` 指令来指定）。



###### ADD

`ADD` 指令与 [COPY](https://www.quanxiaoha.com/docker/dockerfile-copy-file.html) 指令功能类似，都可以复制文件或文件夹，不同的是`ADD` 指令在 `COPY` 的基础之上加了一些功能：

-  `源路径`可以是一个 URL, 这种情况下，Docker 引擎会去下载 URL 对应的文件并放到 `目标路径` 下。
- 当 `源路径` 是一个压缩文件，如 `tar` 、`gzip` 、 `bzip2` 、`xz` 等， `ADD` 指令将自动解压此文件到 `目标路径` 下。

> Docker 官方文档中更推荐使用 `COPY` , 因为 `COPY` 语义更加明确，乍一看就知道是复制文件，而 `ADD` 则包含了很多复杂的功能，行为不够清晰。另外，`ADD` 指令会让构建缓存失效，从而会让镜像构建变得缓慢。
>
> 有自动解压缩的需求时，适合使用 `ADD` 指令



###### CMD

用于启动容器时，指定需要运行的程序以及参数。

```dockerfile
CMD ["<可执行文件>", "<参数1>", "<参数2>", ...] # 官方推荐格式
```

> 此种格式在解析时会被解析成 JSON 数组，因此一定要使用双引号 " , 而不是单引号 ' 。

如果Dockerfile中存在多个CMD指令，仅最后一个生效。



###### ENTRYPOINT

`ENTRYPOINT` 的功能和`CMD`一样，都用于指定容器启动程序以及参数。

> 和CMD一样，若存在多个ENTRYPOINT指令，仅最后一个生效。

**ENTRYPOINT 和 CMD 的不同之处**

对于 `CMD` 指令， 执行 `docker run` 命令如果有传递参数，这些参数会覆盖 Dockerfile 中的`CMD` 指令参数，但是对于 `ENTRYPOINT` 来说，这些参数会被传递给 `ENTRYPOINT`，而不是覆盖。

CMD指令为：`CMD [ "curl", "-s", "http://myip.ipip.net" ]`

执行`docker run myip -i`

实际执行的就是`docker run myip -i`而不是`docker run myip curl -s http://myip.ipip.net -i`

这个时候 `ENTRYPOINT` 就上场了, 因为它可以传递参数，而不是覆盖。