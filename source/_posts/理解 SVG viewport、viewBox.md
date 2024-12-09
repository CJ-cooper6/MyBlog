---
title: 理解 SVG viewport、viewBox
date: 2024-09-18 17:57:23
tags: Svg
---

# 理解 SVG viewport、viewBox

### viewport

表示 SVG 可见区域的大小，可以想象成一个画布。

```
<svg width="500" height="300"></svg>
```

和div、span元素类似，可以使用em、ex、px等单位。

### viewBox

`viewBox`属性有4个值：

```
viewBox="x, y, width, height"  // x:左上角横坐标，y:左上角纵坐标，width:宽度，height:高度
```

viewbox根据四个参数在画布上截取一个矩形，然后把截取出来的图像根据画布大小自适应调整。



直观理解：

1.当没有viewBox时：

```
<svg width="400" height="300" style="border:1px solid #cd0000;">
    <rect x="10" y="5" width="20" height="15" fill="#cd0000"/>
</svg>
```

<svg width="400" height="300" style="border:1px solid #cd0000;">
    <rect x="10" y="5" width="20" height="15" fill="#cd0000"/>
</svg>



2.`viewBox="0,0,40,30"`相当于在SVG上圈了下图左上角所示的一个框框：

<svg width="400" height="300" style="border:1px solid #cd0000;">
  <rect x="0" y="0" width="40" height="30" stroke="#cd0000" fill="white"/>
  <rect x="10" y="5" width="20" height="15" fill="#cd0000"/>
</svg>



3.然后根据画布的大小自适应调整（viewBox小于viewport,将框中的图像调整到画布中相当于放大了）：

```
<svg width="400" height="300" viewBox="0,0,40,30" style="border:1px solid #cd0000;">
    <rect x="10" y="5" width="20" height="15" fill="#cd0000"/>
</svg>
```

<svg width="400" height="300" viewBox="0,0,40,30" style="border:1px solid #cd0000;">
    <rect x="10" y="5" width="20" height="15" fill="#cd0000"/>
</svg>