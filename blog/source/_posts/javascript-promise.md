---
title: javascript-promise
date: 2024-05-05 18:00:38
tags: 
    - js
    - promise
category: js
excerpt: 详解js的promise机制
---

# JavaScript Promise 状态与方法详解

## Promise 的三种状态

Promise 对象有以下三种状态：

- **待定（pending）**：初始状态，既没有被兑现，也没有被拒绝。
- **已兑现（fulfilled）**：意味着操作成功完成。
- **已拒绝（rejected）**：意味着操作失败。

{% asset_img promises.png promise流程 %}

## `.then()` 方法

`.then()` 方法用于处理 Promise 的结果。它最多接受两个参数：

1. 第一个参数是 Promise 兑现时的回调函数。
2. 第二个参数是 Promise 拒绝时的回调函数。

每个 `.then()` 返回一个新的 Promise 对象，可以用于链式调用。

## Promise 并发控制

Promise 类提供了四个静态方法来促进异步任务的并发：

### `Promise.all()`

在所有传入的 Promise 都被兑现时兑现；在任意一个 Promise 被拒绝时拒绝。

### `Promise.allSettled()`

在所有的 Promise 都被敲定时兑现，无论它们是被兑现还是被拒绝。

### `Promise.any()`

在任意一个 Promise 被兑现时兑现；仅在所有的 Promise 都被拒绝时才会拒绝。

### `Promise.race()`

在任意一个 Promise 被敲定时敲定。换句话说，在任意一个 Promise 被兑现或被拒绝时立即返回。

## 示例代码

下面是一个完整的示例，展示了如何使用 Promise 处理异步操作及其错误处理。

```javascript
// 为了尝试错误处理，使用“阈值”值会随机地引发错误。
const THRESHOLD_A = 8; // 可以使用 0 使错误必现

function tetheredGetNumber(resolve, reject) {
    console.log('执行了tetheredGetNumber', resolve, reject);
    setTimeout(() => {
        const randomInt = Date.now(); // 当前时间戳
        const value = 7;
        if (value < THRESHOLD_A) { // 小于8的时间
            resolve(value);
        } else {
            reject(`太大了：${value}`);
        }
    }, 500);
}

function determineParity(value) {
    console.log('执行了determineParity', value);
    const isOdd = value % 2 === 1; // 判断是否为奇数
    return { value, isOdd };
}

function troubleWithGetNumber(reason) {
    console.log('执行了troubleWithGetNumber', reason);
    const err = new Error("获取数据时遇到问题", { cause: reason });
    console.error(err);
    throw err;
}

function promiseGetWord(parityInfo) {
    console.log('执行了promiseGetWord', parityInfo);
    return new Promise((resolve, reject) => {
        const { value, isOdd } = parityInfo;
        if (value >= THRESHOLD_A - 1) { // 7
            reject(`还是太大了：${value}`);
        } else {
            parityInfo.wordEvenOdd = isOdd ? "奇数" : "偶数";
            resolve(parityInfo);
        }
    });
}

new Promise(tetheredGetNumber)
    .then(determineParity, troubleWithGetNumber) // then 接受两个参数，（成功之后执行，失败之后执行）
    .then(promiseGetWord)
    .then((info) => {
        console.log(`得到了：${info.value}, ${info.wordEvenOdd}`);
        return info;
    })
    .catch((reason) => {
        if (reason.cause) {
            console.error("已经在前面处理过错误了");
        } else {
            console.error(`运行 promiseGetWord() 时遇到问题：${reason}`);
        }
    })
    .finally(() => console.log("所有回调都完成了"));
```

### 解释

1. **`tetheredGetNumber`**：模拟异步操作，使用 `setTimeout` 模拟延迟，并根据阈值决定是兑现还是拒绝 Promise。
2. **`determineParity`**：检查数字是奇数还是偶数，并返回包含该信息的对象。
3. **`troubleWithGetNumber`**：处理 Promise 被拒绝的情况，抛出一个新的错误。
4. **`promiseGetWord`**：根据阈值决定是否继续兑现 Promise 或拒绝它，并添加额外的信息到对象中。
5. **链式调用**：通过 `.then()` 方法处理成功和失败的结果，并最终使用 `.catch()` 和 `.finally()` 进行错误处理和清理工作。
