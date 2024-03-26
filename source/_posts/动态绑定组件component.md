---
title: 动态绑定组件component
date: 2024/3/26 16:35:25
---

# 动态绑定组件component

<component></component>标签是Vue框架自定义的标签，它的用途就是可以动态绑定我们的组件，component通过属性is的值可以渲染不同的组件。

```vue
<template>
  <div class="dashboard-container">
    <component :is="currentRole" />
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import adminDashboard from './admin'
import editorDashboard from './editor'

export default {
  name: 'Dashboard',
  components: { adminDashboard, editorDashboard },
  data() {
    return {
      currentRole: 'adminDashboard'
    }
  },
  computed: {
    ...mapGetters([
      'roles'
    ])
  },
  created() {
    if (!this.roles.includes('admin')) {
      this.currentRole = 'editorDashboard'
    }
  }
}
</script>
```

