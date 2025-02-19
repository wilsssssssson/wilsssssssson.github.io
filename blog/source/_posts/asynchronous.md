---
title: asynchronous
date: 2024-05-17 15:44:42
tags: 
    - js
    - multi-process
category: js
excerpt: js利用浏览器的多线程模拟异步操作
---
# 浏览器多线程与 JavaScript 异步操作

## 浏览器多线程

浏览器通过多个线程来处理不同的任务，以下是主要的线程及其功能：

### 主要线程

- **GUI 渲染线程**：负责渲染和解析页面内容。
- **JS 引擎线程**：负责解析和执行 JavaScript 代码。浏览器只为每个标签页分配一个 JS 引擎线程，因此它是单线程的。
- **定时器监听线程**：负责管理 `setTimeout` 和 `setInterval` 等定时器操作。
- **事件监听线程**：负责监听用户交互事件（如点击、键盘输入等）并触发相应的回调函数。
- **HTTP 网络请求线程**：用于处理网络请求。在同一源下，浏览器通常最多分配 5-7 个网络请求线程。

### 其他线程

浏览器还可能有其他线程，例如：
- WebSocket 线程
- 文件读取线程

## JavaScript 异步操作

JavaScript 是单线程语言，但它可以通过异步编程模型实现非阻塞操作。这主要依赖于事件循环机制（Event Loop）以及微任务（Microtasks）和宏任务（Macrotasks）的概念。

### 异步微任务

微任务在当前任务完成后立即执行，优先级较高。常见的微任务包括：

- `requestAnimationFrame`
- `Promise`
- `async/await`
- `queueMicrotask`
- `MutationObserver`
- `IntersectionObserver`

### 异步宏任务

宏任务在每次事件循环的末尾执行，优先级较低。常见的宏任务包括：

- `setTimeout`
- `setInterval`
- 事件绑定（如点击事件）

### 事件循环机制

JavaScript 中的异步操作是通过浏览器的多线程机制和基于事件循环（Event Loop）的机制来实现的。以下是事件循环的基本流程：

1. **执行全局脚本**：首先执行全局脚本中的同步代码。
2. **执行微任务队列**：当全局脚本执行完毕后，会依次执行所有微任务队列中的任务。
3. **执行宏任务队列**：微任务队列执行完毕后，会从宏任务队列中取出一个任务执行。
4. **重复步骤 2 和 3**：不断重复执行微任务和宏任务队列中的任务，直到所有任务都完成。

{% asset_img image.png This is an example image %}