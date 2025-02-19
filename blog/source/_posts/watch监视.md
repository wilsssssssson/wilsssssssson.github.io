---
title: 'watch监视'
date: 2024-05-22 19:30:39
tags: 
    - watch
    - vue3

category: 
    - vue3
    - watch
excerpt: watch，watchweffect,subscribe的使用方法
---
## Vue.js Watch 监视器使用详解

### 监视对象类型

- **函数**：返回一个值。
- **Ref**：监视由 `ref` 定义的对象类型数据时，实际上是在监视对象的地址值。若要监视对象内部属性的变化，需手动开启深度监视。
- **响应式对象**：当监视响应式对象中的某个基本类型的属性时，需要以函数的形式来定义。

此外，还可以监视由上述类型组成的数组。

[Vue.js官方文档](https://cn.vuejs.org/api/reactivity-core.html#watch)

### 参数说明

- `immediate`: 在侦听器创建时立即触发回调。第一次调用时旧值是 `undefined`。
- `deep`: 如果源是对象，强制深度遍历以便在深层级变更时触发回调。
- `flush`: 调整回调函数的刷新时机，可参考回调的刷新时机及 `watchEffect()`。
- `onTrack / onTrigger`: 用于调试侦听器的依赖关系。
- `once`: 回调函数只会运行一次，侦听器将在回调函数首次运行后自动停止。

> 注意：`watchEffect` 可实现监视页面的所有属性，并且可以实现页面懒加载。

### 订阅 (`subscribe`) 实例

```javascript
talkStore.$subscribe((mutation, state) => {
    console.log('talkStore里面保存的数据发生了变化', mutation, state);
    localStorage.setItem('talkList', JSON.stringify(state.talkList));
});