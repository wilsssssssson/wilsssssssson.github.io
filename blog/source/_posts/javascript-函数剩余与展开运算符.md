---
title: javascript-函数剩余与展开运算符
date: 2024-03-28 09:05:23
tags: 
    - js 
    - 传参
category: js
excerpt: 函数传参中经常经常用到的不定参数，接受方法，剩余参数和展开运算符
---

# 函数剩余参数和展开运算符

## 1. 动态传参

在JavaScript中，函数可以通过`arguments`对象来接收动态数量的参数。这是一个类数组对象，包含传递给函数的所有参数。

```javascript
function add() {
    console.log(arguments);
}
add(1, 2, 3, 4); // 可以传入任意数量的参数
// `arguments` 对象包含了传入的所有参数，但它是伪数组类型
```

## 2. 剩余运算符（Rest Operator）

剩余运算符允许我们将一个不定数量的参数表示为一个数组。它使用三个点`...`前缀，并且必须是函数的最后一个参数。

```javascript
function getSum(a, b, ...arr) {
    console.log(arr); // 输出除a和b外的所有参数作为一个真数组
}
getSum(1, 2, 3, 4, 5); // arr 将输出 [3, 4, 5]
```

注意：与`arguments`不同，通过剩余运算符得到的`arr`是一个真正的数组，可以直接使用数组的方法。

## 3. 展开运算符（Spread Operator）

展开运算符也使用三个点`...`，但它用于在调用函数或构建数组时展开数组（或其他可迭代对象）。

### 典型应用示例：

- **求最大最小值**:
  ```javascript
  const numbers = [1, 2, 3, 4, 5];
  console.log(Math.max(...numbers)); // 使用展开运算符展开数组，找到最大值
  ```
  
- **合并数组**:
  ```javascript
  const arr1 = [1, 2, 3];
  const arr2 = [4, 5, 6];
  const combinedArr = [...arr1, ...arr2]; // 合并两个数组，不修改原数组
  ```

展开运算符不会修改原来的数组，而是创建一个新的数组。
