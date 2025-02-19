---
title: lazyLoading
date: 2024-06-13 13:30:51
tags: 
  - vue3
  - Hook
category: 
  - vue3
  - Hook
excerpt: 在Vue应用中，可以通过监听`scroll`事件和利用组件的生命周期钩子来实现数据的懒加载。下面是一个简单的示例，展示了如何实现这一功能
---
# 使用Vue生命周期钩子实现懒加载

在Vue应用中，可以通过监听`scroll`事件和利用组件的生命周期钩子来实现数据的懒加载。下面是一个简单的示例，展示了如何实现这一功能。

## 代码示例

### 完整代码

```javascript
export default {
  data() {
    return {
      dataList: [], // 初始数据列表
      isLoading: false, // 加载状态
      page: 1, // 当前页码
    };
  },
  mounted() {
    this.loadMoreData();
    window.addEventListener('scroll', this.handleScroll);
  },
  methods: {
    loadMoreData() {
      this.isLoading = true;
      // 模拟数据加载
      setTimeout(() => {
        // 假设每次加载5条数据
        const newData = Array.from({ length: 5 }, (_, index) => ({
          id: this.dataList.length + index + 1,
          content: `数据 ${this.page + index}`,
        }));
        this.dataList.push(...newData);
        this.isLoading = false;
        this.page++;
      }, 1000); // 利用setTimeout模拟加载数据，实际应替换为HTTP请求
    },
    handleScroll() {
      // 判断是否滚动到底部
      const scrollElement = this.$refs.scrollContainer;
      if (
        scrollElement.scrollHeight - scrollElement.scrollTop ===
        scrollElement.clientHeight
      ) {
        if (!this.isLoading) {
          this.loadMoreData();
        }
      }
    },
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll);
  },
};