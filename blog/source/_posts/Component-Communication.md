---
title: Component Communication
date: 2024-05-14 11:24:11
tags: 
    - Component Communication
    - vue3
category: vue3
excerpt: Vue.js 组件之间通信概念详解
---
# Vue.js 组件之间通信概念详解

## 目录
1. Props
2. 自定义事件
3. mitt（略）
4. v-model
5. $attrs
6. $refs、$parent
7. provide、inject
8. Pinia
9. Slot

## 1. Props (父传子数据，子传父)
Props用于父组件向子组件传递数据。子组件通过父亲的方法实现数据回传。
- **Father Component**
    ```html
    <Child :car="car" :sendToy="getToy"/>
    ```
- **Children Component**
    ```javascript
    defineProps(['car','sendToy'])
    ```

## 2. 自定义事件 (子传父)
通过自定义事件可以将方法从父组件传递给子组件以实现子到父的数据传输。
- **Father Component**
    ```html
    <Child @send-toy="saveToy"/>
    ```
- **Children Component**
    ```javascript
    const emit = defineEmits(['send-toy']);
    // 触发事件
    <button @click="emit('send-toy', toy)">Send Toy</button>
    ```

## 4. v-model
v-model用于实现双向数据绑定，可以在HTML标签或组件标签上使用。
- **示例**
    ```html
    <AtguiguInput v-model:ming="username" v-model:mima="password"/>
    ```

## 7. Provide & Inject
Provide允许祖先组件向其所有后代组件提供数据，而Inject则让后代组件接收这些数据。
- **Ancestor Component**
    ```javascript
    provide('moneyContext', {money, updateMoney})
    ```
- **Descendant Component**
    ```javascript
    let {money, updateMoney} = inject('moneyContext', {money:0, updateMoney:(param:number)=>{}})
    ```

更多关于Pinia和其他Vue.js核心概念的详细解释将在后续部分中介绍。