---
title: RN-连接初始化
date: 2024-07-01 13:20:02
tags: RN
category: RN
excerpt: react native初始化连接
---

# MUMU模拟器与Hermes调试

## 连接MUMU模拟器
```bash
adb connect 127.0.0.1:7555
```

## 开发者菜单，用于调试
```bash
adb shell input keyevent 82
```

## 使用Hermes打开控制台或在Node.js中查看输出

### 在 Chrome 浏览器中操作
1. 导航到 `chrome://inspect`。
2. 使用 "Configure..." 按钮添加开发服务器地址（通常是 `localhost:8081`）。
3. 现在应该能看到一个带有 "inspect" 链接的 "Hermes React Native" 目标。点击这个链接打开调试器。
```
