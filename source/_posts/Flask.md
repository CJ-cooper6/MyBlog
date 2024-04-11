---
title: Flask
date: 2024-01-04 18:15:46
tags: Python
---

# Flask

MVT模型，model、view、template

## 路由

**route()**装饰器用于将URL绑定到函数



## 模版

- 模板其实是一个包含响应文本的文件,其中用占位符(变量)表示动态部分,告诉模板引擎其具体的值需要从使用的数据中获取
- 使用真实值替换变量,再返回最终得到的字符串,这个过程称为 **渲染**
- Flask 是使用 **Jinja2** 这个模板引擎来渲染模板

render_template 函数渲染模版

## 蓝图

使用场景:

- 把一个应用分解为一个蓝图的集合。这对大型应用是理想的。一个项目可以实例化 一个应用对象，初始化几个扩展，并注册一集合的蓝图。
- 以 URL 前缀和/或子域名，在应用上注册一个蓝图。 URL 前缀/子域名中的参数即 成为这个蓝图下的所有视图函数的共同的视图参数（默认情况下）。
- 在一个应用中用不同的 URL 规则多次注册一个蓝图。
- 通过蓝图提供模板过滤器、静态文件、模板和其它功能。一个蓝图不一定要实现应 用或者视图函数。
- 初始化一个 Flask 扩展时，在这些情况中注册一个蓝图。

Flask 中的蓝图不是即插应用，因为它实际上并不是一个应用——它是可以注册，甚至 可以多次注册到应用上的操作集合。为什么不使用多个应用对象？你可以做到那样 （见 应用调度 ），但是你的应用的配置是分开的，并在 WSGI 层管理。

蓝图作为 Flask 层提供分割的替代，共享应用配置，并且在必要情况下可以更改所 注册的应用对象。它的缺点是你不能在应用创建后撤销注册一个蓝图而不销毁整个 应用对象。



基本蓝图使用方法：

```python
from flask import Blueprint, render_template, abort
from jinja2 import TemplateNotFound

simple_page = Blueprint('simple_page', __name__,
                        template_folder='templates')

@simple_page.route('/', defaults={'page': 'index'})
@simple_page.route('/<page>')
def show(page):
    try:
        return render_template('pages/%s.html' % page)
    except TemplateNotFound:
        abort(404)
```

