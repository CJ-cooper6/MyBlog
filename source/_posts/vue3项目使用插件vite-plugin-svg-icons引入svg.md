---
title: vue3项目使用插件vite-plugin-svg-icons引入svg
date: 2024-12-09 17:10:46
tags: ["前端", "Vue", "Svg"]
---

# vue3项目使用插件vite-plugin-svg-icons引入svg

## 安装插件

```
yarn add vite-plugin-svg-icons
或
npm install vite-plugin-svg-icons
```

## 配置 Vite
在 vite.config.ts 中配置插件。你需要引入插件并在 plugins 数组中使用它。
```ts
import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";
import { createSvgIconsPlugin } from "vite-plugin-svg-icons";
import path from "path";

export default defineConfig({
  plugins: [
    vue(),
    createSvgIconsPlugin({
      // 指定图标文件夹
      iconDirs: [path.resolve(process.cwd(), "src/assets/icons")],
      // 指定symbolId格式
      symbolId: "icon-[name]",
    }),
  ],
  server: {
    host: "0.0.0.0",
    port: 5173,
  },
});
```

## 修改 main.ts
```ts
import "./assets/styles/main.css";
//导入插件
import "virtual:svg-icons-register";

import { createApp } from "vue";
import App from "./App.vue";
import pinia from "./stores/index.js";

const app = createApp(App);

app.use(pinia);
app.mount("#app");

```


## 添加 SVG 图标
将你的 SVG 图标文件放在 src/assets/icons 目录下。插件会自动扫描这个目录并生成相应的图标。

## 使用 SVG 图标

1、在 Vue 组件中，可以使用 `<svg>` 和 `<use>` 标签来引用图标。确保属性值与配置中的格式一致。
```ts
<svg style="width: 600px; height:600px">
    <use xlink:href="#icon-phone" fill="red"></use>
</svg>
```

2、封装一个SvgIcon组件
```vue
<template>
  <svg aria-hidden="true" :width="width" :height="height">
    <use :xlink:href="symbolId" :fill="color" />
  </svg>
</template>

<script setup lang="ts">
import { computed } from "vue";

const props = defineProps({
  prefix: {
    type: String,
    default: "icon",
  },
  name: {
    type: String,
    required: true,
  },
  color: {
    type: String,
    default: "",
  },
  width: {
    type: String,
    default: "16px",
  },
  height: {
    type: String,
    default: "16px",
  },
});

const symbolId = computed(() => `#${props.prefix}-${props.name}`);
</script>

```

使用：
```vue
<SvgIcon name="select" />
```