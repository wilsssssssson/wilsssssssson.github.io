---
title: RN-类的使用
date: 2025-02-19 16:47:29
tags: RN
category: RN
excerpt:  React Native 状态管理：函数组件 vs 类组件
---

# React Native 状态管理：函数组件 vs 类组件

在React Native中，状态（`state`）的管理可以通过函数组件使用`useState`和`useEffect`钩子来实现，也可以通过类组件的传统方式来处理。以下分别展示了这两种方式的具体实现。

## 使用函数组件与Hooks

```jsx
const Index = () => {  
  const [statusBarColor, setStatusBarColor] = useState('green');  //react中常用的响应式方法
  
  useEffect(() => {  // 使用useEffect Hook监听statusBarColor的变化，当其变化时执行回调函数
    StatusBar.setBackgroundColor(statusBarColor);  
  }, [statusBarColor]);// 只有当statusBarColor改变时才会触发此effect
  
  const toggleStatusBarColor = () => {  
    const newColor = statusBarColor === 'green' ? 'red' : 'green';  
    setStatusBarColor(newColor);  
  };  
  
  return (  
    <View style={styles.container}>  
      <Switch  
        trackColor={{ false: 'gray', true: 'green' }}  
        thumbColor="blue"  
        onValueChange={toggleStatusBarColor}  
        value={statusBarColor==='green'}  
      />  
    </View>  
  );  
}
```

## 使用类组件

```jsx
export default class Index extends Component {  
  constructor(props) {  
    super(props);  // 调用父类构造器
    this.state = {  // 初始化state对b
      statusBarColor: 'green',  // 状态栏颜色初始为绿色
      switchValue: true  // 开关初始值为true（开）
    };  
  }  


  
  // 组件更新后自动调用，检查状态变化并作出相应操作
  componentDidUpdate(prevProps, prevState) {  
    if (prevState.statusBarColor !== this.state.statusBarColor) {  // 如果状态栏颜色发生了变化
      StatusBar.setBackgroundColor(this.state.statusBarColor);  // 设置状态栏背景颜色
    }  
  }  
  
  // 切换状态栏颜色的方法
  toggleStatusBarColor = () => {  
    const newColor = this.state.statusBarColor === 'green' ? 'red' : 'green';  // 切换颜色
    this.setState({  // 更新状态
      statusBarColor: newColor,  
      switchValue: !this.state.switchValue  // 同步更新switch的状态
    });  
  };  
  
  render() {  //react的render在每次组件的state和props改变的时候，调用该函数
    return (  
      <View style={styles.container}>  
        <Switch  
          trackColor={{ false: 'gray', true: 'green' }}  
          thumbColor="blue"  
          onValueChange={this.toggleStatusBarColor}  
          value={this.state.switchValue}  
        />  
      </View>  
    );  
  }  
}
```
