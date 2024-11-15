---
title: Ptyhon Flask 模版引擎 block
date: 2024-11-15 18:15:46
tags: Python
---

在模板引擎中，像 `{% block %}` 和 `{% endblock %}` 这样的标记通常用于定义和结束模板中的一个块（block）。下面是关于这两个标记的解释：

- `{% block %}`：`block` 标记用于指定一个可以在子模板中被重写或填充的区域。在父模板中使用 `{% block block_name %}` 来定义一个块，`block_name` 可以是任何合法的名称。
- `{% endblock %}`：`endblock` 标记用于结束一个块的定义。在模板中，所有位于 `{% block %}` 和 `{% endblock %}` 标记之间的内容将作为初始内容，可以被子模板继承、重写或覆盖。

模板引擎通过这种方式实现模板的继承和重用。父模板中的 `{% block %}` 定义了一些初始内容，而子模板可以继承这些内容，并通过重写父模板中的 `{% block %}` 块来修改或补充内容，从而实现模板的定制和扩展。

以下是一个简单的例子，演示了父模板和子模板之间如何使用 `{% block %}` 和 `{% endblock %}`：

**父模板（parent_template.html）：**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <title>{% block title %}Default Title{% endblock %}</title>
</head>
<body>
    <div class="content">
        {% block content %}Default Content{% endblock %}
    </div>
</body>
</html>
```

**子模板（child_template.html）：**

```
{% extends "parent_template.html" %}

{% block title %}New Title{% endblock %}

{% block content %}
    <p>This is the customized content.</p>
{% endblock %}
```

在这个例子中，子模板 `child_template.html` 继承了父模板 `parent_template.html`，并重写了父模板中的两个块 `title` 和 `content`。这样子模板就可以覆盖父模板中定义的内容，实现定制化的页面展示。