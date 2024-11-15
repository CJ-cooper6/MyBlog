---
title: Python创建空列表使用list()和[]的区别
date: 2024-11-15 10:10:46
tags: Python
---

# Python创建空列表使用list()和[]的区别

list(): 调用函数来创建列表
[]：不需要通过调用函数来创建

[]会被解释器直接识别，而list()解释器会去各个作用域依次查找，如果没有重新定义才会调用内置的初始化空列表函数，毕竟，下面这样定义list()也是可以的，会执行自己定义的list()。

def list():
    return 'hhh'
print(type(list()))

输出：
<class ‘str’>

因此[]比list()的效率要高不少，建议使用[]。



https://www.zhihu.com/question/457831785

https://blog.csdn.net/lycwhu/article/details/125252393

https://broken.blog.csdn.net/article/details/127611701?spm=1001.2101.3001.6650.5&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-5-127611701-blog-103315017.235%5Ev38%5Epc_relevant_sort&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-5-127611701-blog-103315017.235%5Ev38%5Epc_relevant_sort&utm_relevant_index=10

https://blog.csdn.net/OnePiece_97/article/details/103315017