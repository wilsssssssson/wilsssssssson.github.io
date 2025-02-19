---
title: slot
date: 2024-06-13 14:51:02
tags: 
    - vue3
    - slot
category: vue3
excerpt: Vue 插槽（Slots）详解，介绍一些不同的插槽以及基本代码
---

# Vue 插槽（Slots）详解

## 默认插槽

### 定义
```html
<slot>默认内容</slot>
```

### 使用
```html
<Category title="今日影视推荐">
    <video :src="videoUrl" controls></video>
</Category>
```

## 具名插槽

### 定义
```html
<div class="category">
    <slot name="s1">默认内容1</slot>
    <slot name="s2">默认内容2</slot>
</div>
```

### 使用
```html
<Category>
    <template v-slot:s2>
        <img :src="imgUrl" alt="">
    </template>
    <template v-slot:s1>
        <h2>今日美食城市</h2>
    </template>
</Category>
```

## 作用域插槽 (父亲决定孩子的样式，但是数据还是儿子自己的)

### 子组件
```html
<slot :youxi="games" x="哈哈" y="你好"></slot>
```

### 父组件
```html
<Game>
    <template v-slot="params">
        <!-- params 可以自定义 -->
        <ul>
            <li v-for="y in params.youxi" :key="y.id">
                {{ y.name }}
            </li>
        </ul>
    </template>
</Game>
```

### 综合使用
```html
<template v-slot:name="params">
<!-- 其中 name 是具名插槽的名字，params 是子组件传过来的数据 -->
```
