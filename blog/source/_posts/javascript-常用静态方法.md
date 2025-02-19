---
title: javascript-常用静态方法
date: 2024-03-24 16:10:35
tags: 
    - js
    - 静态方法
category: js
excerpt: javascript常用的一些静态方法，一般用于来处理数组，迭代遍历等操作
---
# JavaScript常用静态方法

JavaScript提供了多种方法来操作对象和数组，下面是一些常用的方法及其使用示例。

## 对象操作

### 1. `Object.keys` - 获取所有属性名

`Object.keys` 方法返回一个给定对象自身可枚举属性的数组。

```javascript
const person = {name: 'Alice', age: 25};
console.log(Object.keys(person)); // 输出: ['name', 'age']
```

### 2. `Object.values` - 获取所有属性值

`Object.values` 方法返回一个给定对象自身可枚举属性值的数组。

```javascript
const person = {name: 'Alice', age: 25};
console.log(Object.values(person)); // 输出: ['Alice', 25]
```

### 3. 拷贝对象并添加属性

`Object.assign` 方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。

```javascript
const target = {};
const source = {name: 'Alice', age: 25};
Object.assign(target, source);
target.address = 'Wonderland'; // 添加新属性
console.log(target); // 输出: { name: 'Alice', age: 25, address: 'Wonderland' }
```

## 数组操作

### 1. `forEach` - 遍历数组

`forEach` 方法允许你遍历数组中的每个元素，并对它们执行一个函数。

```javascript
const numbers = [1, 2, 3, 4, 5];
numbers.forEach(number => {
    console.log(number);
});
```
偷偷卷！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！
此代码会依次输出数组中的每个数字。

### 2. `filter` - 过滤数组

`filter` 方法用于创建一个新数组，包含通过所提供函数实现的测试的所有元素。

```javascript
const numbers = [1, 2, 3, 4, 5];
const evenNumbers = numbers.filter(number => number % 2 === 0);
console.log(evenNumbers); // 输出: [2, 4]
```

这段代码筛选出所有偶数并存储在`evenNumbers`中。

### 3. `map` - 迭代数组

`map` 方法创建一个新数组，其结果是对调用数组中的每一个元素调用一个提供的函数后的返回值。

```javascript
const numbers = [1, 2, 3, 4, 5];
const squaredNumbers = numbers.map(number => number * number);
console.log(squaredNumbers); // 输出: [1, 4, 9, 16, 25]
```

这会生成一个新的数组，其中每个元素都是原数组对应位置元素的平方。

### 4. `reduce` - 累计器

`reduce` 方法对数组中的每个元素执行一个由您提供的reducer函数（升序执行），将其结果汇总为单个返回值。

```javascript
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((accumulator, currentValue) => accumulator + currentValue, 0);
console.log(sum); // 输出: 15
```

在这个例子中，`reduce` 将数组中的所有数值相加，从起始值`0`开始累加。
{% asset_img  image1.png 有趣的例子 %}
{% asset_img  image2.png 有趣的例子 %}