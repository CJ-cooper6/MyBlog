---
title: 浏览器解析href地址规则
date: 2024-06-14 10:10:46
---



如果路径以`/`开头，则表示绝对路径，从站点根目录开始解析。

如果路径不以`/`开头，则表示相对路径，从当前页面的URL所在目录开始解析。在解析相对路径时，会将当前URL的域名、路径部分保留，只替换路径最后的一部分内容。如：

```
此时url是 http://localhost:5000/user/resources/subject-libs#/personal-subject/61

执行 window.location.href = "subject" 
会跳转到： http://localhost:5000/subject


执行 window.location.href = "subject" 
会跳转到： http://localhost:5000/user/resources/subject

```

