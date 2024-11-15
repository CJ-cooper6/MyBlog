---
title: input、textarea 实现高度宽度随文本内容自动变更
date: 2024-11-15 18:15:46
tags: 前端
---

实现原理：给textarea套上外容器，使用绝对定位，设置`height:100%; width:100%;` 这样textarea就可以随着外容器的高度变化而变化。再用块级元素填充文字，块元素可以随着文本内容自动变更高度宽度。设置块元素`visibility: hidden;`即可。

代码：
```html
<div class="tree-content-with-tooltip">
    <span class="content">{{ nodeText }}</span>
    <textarea
      class="tree-textarea"
      @blur="handleBlur"
      @keydown.enter="setBlur"
      v-model="nodeText"
      @mousedown.stop="startEditing"
      @keydown="onKeyDown"
      ref="editCtrl"
    ></textarea>
</div>

/* css */
.tree-content-with-tooltip {
  position: relative;
 	width: 100%;
}

.content {
    display: block;
    overflow: hidden;
    visibility: hidden;
    white-space: pre-wrap;
}

.tree-textarea {
  height: 100%;
  border: unset;
  position: absolute;
  width: 100%;
  margin: 0;
  left: 0;
  top: 0;
  overflow: hidden;
  padding: 0;
}

```