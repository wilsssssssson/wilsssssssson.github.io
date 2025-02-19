---
title: 'lifeCycle'
date: 2024-05-12 13:22:01
tags: 
    - vue3
    - lifeCycle
    - Hook
category: 
    - vue3
    - Hook
excerpt: 生命周期钩子函数使用笔记,主要介绍一些生命周期，以及之间的时间顺序
---
# Vue 生命周期钩子函数使用笔记

当我们将这些生命周期钩子函数写在自定义Hooks里面时，意味着只要组件引用了这个Hooks，相应的生命周期事件就会自动绑定到该组件上。

## 生命周期钩子示例代码

### 挂载阶段

- **挂载前**

  ```javascript
  onBeforeMount(() => {
    // console.log('挂载前')
  });
  ```

- **挂载完毕**

  ```javascript
  onMounted(() => {
    console.log('子---挂载完毕');
  });
  ```

### 更新阶段

- **更新前**

  ```javascript
  onBeforeUpdate(() => {
    // console.log('更新前')
  });
  ```

- **更新完毕**

  ```javascript
  onUpdated(() => {
    // console.log('更新完毕')
  });
  ```

### 卸载阶段

- **卸载前**

  ```javascript
  onBeforeUnmount(() => {
    // console.log('卸载前')
  });
  ```

- **卸载完毕**

  ```javascript
  onUnmounted(() => {
    // console.log('卸载完毕')
  });
  ```

{% asset_img image.png This is an example image %}