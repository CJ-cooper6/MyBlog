---
title: 使用Nginx方向代理，加载不到静态文件
date: 2024-11-15 18:15:46
tags: nginx
---

# 使用Nginx方向代理，加载不到静态文件



用docker部署了一个web服务，可以通过 http://127.0.0.1:9000 访问。
现在想要通过https://xxxx.com/web 这种方式访问web服务，nginx增加以下配置：

```
location /web { 
proxy_pass http://127.0.0.1:9000; 
proxy_set_header Host $host;
proxy_set_header X-Real-IP $remote_addr; 
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
}
```

这样访问正常返回html页面没有报错，但是静态文件无法加载，查看控制台访问静态资源url不是预期的https://xxxx.com/web这样的url。

![[Pasted image 20241114211906.png]]


网页再次请求js和css以及其他静态资源不会带上二级路径/web，没有找到什么好的解决方法。最后是通过反向代理端口的方式解决了：

```shell
server {
	listen 8090 ssl;
    server_name www.xxxxxx.com;

    location / {
        proxy_pass http://127.0.0.1:9001;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    	}
    }
```

直接访问 https://xxxx.com:8090 可以访问到web服务。

参考：
https://segmentfault.com/q/1010000040250200
