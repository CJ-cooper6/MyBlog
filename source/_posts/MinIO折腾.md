---
title: MinIO折腾
date: 2024-04-01 18:15:46
tags: MinIO
---

# MinIO折腾

```
docker pull minio/minio
```



存储文件位置

`mkdir -p /root/minio/data`

配置文件位置

`mkdir -p /root/minio/config`



启动

```
docker run --name minio -p 9000:9000 -p 9001:9001 -d --restart=always -e "MINIO_ACCESS_KEY=xxxxx" -e "MINIO_SECRET_KEY=xxxxxxxxxxx" -v "/root/minio/data":"/data" -v "/root/minio/config":"/root/.minio" minio/minio server /data --console-address ":9001"
```

**注意**：

- 将用户名密码替换你自己设置的，另外ACCESS_KEY至少3位，MINIO_SECRET_KEY至少8位，否则容器启动失败，抛出此异常
- --console-address ":9001" 端口`9001`: 控制台web使用
- 端口`9000`: 上传API使用
- 新版本的Minio需要做两个端口映射，分别是`控制台端口号` 和 `api端口号`



访问 http://127.0.0.1:9001/



使用我们做数据映射时的账号密码，就可以登录进去，然后创建Buckets，将`Access Policy`设置成为`Public`，这样才能通过url访问图片

![image-20240329013438551](https://www.cocokoi.top:9789/images/imgs/2024/03/29/image-20240329013438551.png)



输入`ip + api端口 + 桶名 + 文件名` 即可访问图片：

<img src="https://www.cocokoi.top:9789/images/imgs/2024/03/29/image-20240329013513505.png" alt="image-20240329013513505" style="zoom:50%;" />







### 结合PicGo搭建图床

安装插件

<img src="https://www.cocokoi.top:9789/images/imgs/2024/04/02/image-20240402155325332.png" alt="image-20240402155325332" style="zoom:50%;" />



配置信息

<img src="https://www.cocokoi.top:9789/images/imgs/2024/04/01/image-20240401155717654.png" alt="image-20240401155717654" style="zoom:50%;" />



大功告成！



参考：

https://blog.csdn.net/qq_43198727/article/details/131000772

