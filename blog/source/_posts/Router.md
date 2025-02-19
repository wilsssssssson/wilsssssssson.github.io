---
title: Router
date: 2024-06-23 14:30:13
tags: 
  - vue3
  - Router
category: vue3
excerpt: vue3中路由的概念以及一些使用方法
---

# Vue Router

## 基本用法

### 路由链接和视图显示

#### 路由链接 `<RouterLink>`

`<RouterLink>` 用于导航到不同的路由。以下是几种常见的使用方式：

```html
<!-- 直接指定路径 -->
<RouterLink to="/home" active-class="active">首页</RouterLink>

<!-- 使用名称导航 -->
<RouterLink :to="{name: 'xinwen'}" active-class="active">新闻</RouterLink>

<!-- 使用路径对象 -->
<RouterLink :to="{path: '/about'}" active-class="active">关于</RouterLink>
```

#### 显示路由加载区域 `<RouterView>`

`<RouterView>` 是路由匹配到的组件将要渲染的地方。

```html
<RouterView></RouterView>
```

### 路由配置文件 `index.ts`

在 `index.ts` 文件中配置路由规则：

```javascript
import { createRouter, createWebHistory } from 'vue-router';
import Home from './views/Home.vue';
import News from './views/News.vue';
import Detail from './views/Detail.vue';

const router = createRouter({
  history: createWebHistory(), // 路由器的工作模式
  routes: [ // 路由规则
    {
      name: 'zhuye',
      path: '/home',
      component: Home
    },
    {
      name: 'xinwen',
      path: '/news',
      component: News,
      children: [
        {
          path: 'detail',
          component: Detail
        }
      ]
    }
  ]
});

export default router;
```

## 路由传参

### Query 参数传递

通过 `query` 参数进行传参：

```html
<RouterLink 
  :to="{
    name: 'xiang',
    query: {
      id: news.id,
      title: news.title,
      content: news.content
    }
  }"
>
  新闻详情
</RouterLink>
```

#### 接收参数

**方法1：使用 `props`**

在路由配置中设置 `props` 函数来接收参数：

```javascript
{
  path: '/xiang',
  component: Xiang,
  props(route) {
    return route.query;
  }
}
```

在组件内使用 `defineProps`：

```javascript
defineProps(['id', 'title', 'content']);
```

**方法2：直接使用 `$route`**

```html
<li>编号：{{ $route.query.id }}</li>
<li>标题：{{ $route.query.title }}</li>
<li>内容：{{ $route.query.content }}</li>
```

或者使用组合式API：

```javascript
import { useRoute } from 'vue-router';
import { toRefs } from '@vueuse/core';

export default {
  setup() {
    const route = useRoute();
    const { query } = toRefs(route);
    return { query };
  }
};
```

## 编程式路由导航

可以使用 `router.push()`、`router.replace()` 等方法进行编程式导航：

```javascript
router.replace({
  name: 'xiang',
  query: {
    id: news.id,
    title: news.title,
    content: news.content
  }
});
```

## 路由重定向

在路由配置中添加重定向规则：

```javascript
{
  path: '/',
  redirect: '/home'
}
```