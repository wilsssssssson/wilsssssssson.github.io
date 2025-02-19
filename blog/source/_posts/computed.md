---
title: 'computed'
date: 2024-03-12 16:45:54
tags: 
    - vue3
    - computed
category: vue3
excerpt: 计算属性的使用方法
---
## Vue.js 计算属性 (`computed`) 使用详解

### 计算属性简介

计算属性 (`computed`) 在 Vue.js 中通常用于基于其他响应式数据派生出新的值。默认情况下，计算属性是只读的，即它们只有 `get` 方法而没有 `set` 方法。然而，通过定义一个带有 `get` 和 `set` 方法的对象，可以使计算属性变得可读写。

### 示例代码

下面的例子展示了如何使用 `ref` 创建两个响应式变量 `firstName` 和 `lastName`，并创建一个可读写的计算属性 `fullName`。

```javascript
let firstName = ref('zhang');
let lastName = ref('san');

// 定义一个可读写的计算属性 fullName
let fullName = computed({
  // 当 fullName 被读取时调用 get 方法
  get() {
    return firstName.value.slice(0,1).toUpperCase() + firstName.value.slice(1) + '-' + lastName.value;
  },
  // 当 fullName 被修改时调用 set 方法，并接收新值
  set(val) {
    const [str1, str2] = val.split('-');
    firstName.value = str1;
    lastName.value = str2;
  }
});

// 修改 fullName 的函数
function changeFullName() {
  fullName.value = 'li-si';
}