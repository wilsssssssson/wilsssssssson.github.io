---
title: javascript-变量提升
date: 2024-03-16 17:13:23
tags: 
    - javascript-变量提升
    - js
category: js
excerpt: var的变量函数提升机制
---
# JavaScript 中的变量提升与函数声明提升

## 变量提升（Hoisting）

在 JavaScript 中，使用 `var` 声明的变量会被提升到其所在作用域的最前面，但赋值操作不会被提升。这意味着可以在声明之前访问这些变量，但它们的值会是 `undefined`。

### 示例

```javascript
console.log(num);  // 输出: undefined
var num = 10;

// 实际上相当于：
var num;
console.log(num);  // 输出: undefined
num = 10;
```

### 关键点

- **变量声明**：`var` 声明的变量会被提升到当前作用域的顶部。
- **变量赋值**：赋值操作不会被提升，因此在声明之前访问变量时，其值为 `undefined`。

## 函数声明提升

函数声明也会被提升到其所在作用域的最前面，这意味着你可以在函数声明之前调用该函数。

### 示例

```javascript
console.log(a(2, 3));  // 输出: 5

function a(x, y) {
    return x + y;
}

// 实际上相当于：
function a(x, y) {
    return x + y;
}
console.log(a(2, 3));  // 输出: 5
```

### 函数表达式与函数声明的区别

函数表达式不会像函数声明那样被提升。如果你使用 `var` 来声明一个函数表达式，并在声明之前调用它，会导致错误或输出 `undefined`。

#### 错误示例

```javascript
console.log(a(2, 3));  // 输出: Uncaught TypeError: a is not a function

var a = function add(x, y) {
    return x + y;
};

// 实际上相当于：
var a;
console.log(a(2, 3));  // 输出: Uncaught TypeError: a is not a function
a = function add(x, y) {
    return x + y;
};
```

## 结论

为了避免由于变量提升带来的潜在问题，建议不要使用 `var`，而是使用更现代的 `let` 和 `const` 关键字来声明变量。它们具有块级作用域，且不会导致类似的问题。

### 使用 `let` 和 `const`

- **`let`**：用于声明可以重新赋值的变量，具有块级作用域。
- **`const`**：用于声明不可重新赋值的常量，也具有块级作用域。

### 示例

```javascript
console.log(num);  // 输出: ReferenceError: Cannot access 'num' before initialization
let num = 10;

// 函数表达式同样适用
console.log(add(2, 3));  // 输出: ReferenceError: Cannot access 'add' before initialization
const add = function (x, y) {
    return x + y;
};

通过使用 `let` 和 `const`，可以避免许多由于变量提升引起的问题，并编写更清晰、更安全的代码。
```
