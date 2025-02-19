---
title: javascript-json
date: 2024-04-01 22:52:19
tags: 
  - js
  - JSON
category:
    - js
excerpt: javascript中的json处理一些方法
---

# JavaScript 中的 JSON 处理

JavaScript 内置了对 JSON 的解析支持，允许轻松地在 JSON 和 JavaScript 对象之间进行转换。

## JSON 数据类型

JSON 支持的数据类型包括：

- **number**：与 JavaScript 的 `number` 完全一致。
- **boolean**：即 JavaScript 的 `true` 或 `false`。
- **string**：即 JavaScript 的 `string`。
- **null**：即 JavaScript 的 `null`。
- **array**：使用 JavaScript 的数组表示法 `[]`。
- **object**：使用 JavaScript 的对象表示法 `{ ... }`。

## JSON 转换方法

### `JSON.stringify`

`JSON.stringify` 方法用于将 JavaScript 对象转换为 JSON 字符串。

#### 语法

```javascript
JSON.stringify(value[, replacer [, space]])
```

#### 参数说明

- **value**：要序列化成 JSON 字符串的值。
- **replacer**（可选）：
  - 如果是函数，则每个属性都会经过该函数的转换和处理。
  - 如果是数组，则只有包含在这个数组中的属性名才会被序列化。
  - 如果为 `null` 或未提供，则对象的所有属性都会被序列化。
- **space**（可选）：
  - 指定缩进用的空白字符串，用于美化输出（pretty-print）。
  - 如果参数是个数字，它代表有多少的空格；上限为 10。
  - 如果参数为字符串（当字符串长度超过 10 个字母，取其前 10 个字母），该字符串将被作为空格。
  - 如果该参数没有提供（或者为 `null`），将没有空格。

#### 示例

```javascript
let xiaoming = {
    name: '小明',
    age: 14,
    gender: true,
    height: 1.65,
    grade: null,
    'middle-school': '"W3C" Middle School',
    skills: ['JavaScript', 'Java', 'Python', 'Lisp']
};

let s = JSON.stringify(xiaoming, null, '  ');
console.log(s);
```

### `JSON.parse`

`JSON.parse` 方法用于将 JSON 字符串转换为 JavaScript 对象。

#### 语法

```javascript
JSON.parse(text[, reviver])
```

- **text**：要解析的 JSON 字符串。
- **reviver**（可选）：一个函数，用来转换解析出的键值对。

## 实际应用示例

下面是一个从 API 获取天气信息并将其转换为 JSON 格式的示例：

```javascript
let url = 'https://api.openweathermap.org/data/2.5/forecast?q=Xian,cn&appid=800f49846586c3ba6e7052cfc89af16c';

fetch(url)
    .then(resp => resp.json())
    .then(data => {
        let info = {
            city: data.city.name,
            weather: data.list[0].weather[0].main,
            time: data.list[0].dt_txt
        };
        alert(JSON.stringify(info, null, '  '));
    });
```

这段代码通过调用 OpenWeatherMap API 获取西安的天气预报数据，并提取城市名称、当前天气状况和时间信息