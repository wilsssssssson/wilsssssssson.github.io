---
title: javascript-防抖节流
date: 2024-05-09 11:22:16
tags: 
    - js
    - 防抖
    - 节流
category: js
excerpt: 在网页端容易出现用户频繁点击导致网页抖动或请求平凡发送，这个文章用settime设置计时器实现防抖即节流
---

# JavaScript中的防抖与节流技术

在处理频繁触发的事件（如窗口调整大小、滚动、输入框输入等）时，为了提高性能和用户体验，我们通常会使用防抖（Debounce）或节流（Throttle）技术。下面分别介绍这两种技术的实现方法。

## 防抖 (Debounce)

防抖的基本思想是：当事件被触发后，延迟指定的时间间隔再执行函数，如果在这个时间间隔内该事件又被触发，则重新计时。

### 实现代码示例

```javascript
// 获取元素
const box = document.getElementsByClassName('fangdou')[0];

function numberadd() {
    this.innerHTML = parseInt(this.innerHTML) + 1;
}

// 给元素绑定mousemove事件，并应用防抖
box.addEventListener('mousemove', debounce(numberadd, 500));

function debounce(func, time) {
    let timer;
    return function () {
        if (timer) clearTimeout(timer);
        timer = setTimeout(() => {
            console.log('this', this);
            func.apply(this);
        }, time);
    }
}
```

**注意**: 使用箭头函数可以让`this`上下文自动正确地绑定，因此不需要手动用`apply`方法来绑定`this`。

## 节流 (Throttle)

节流的核心概念是：保证一个函数在一定时间内只执行一次，即使这个时间段内该函数被多次触发。

### 实现代码示例

```javascript
function throttle(func, time) {
    let timer = null;
    return function () {
        if (timer) return;
        timer = setTimeout(() => {
            func.apply(this);
            timer = null; // 清空定时器
        }, time);
    }
}
```
