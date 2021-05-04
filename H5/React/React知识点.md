# React知识点

> 拓展：
>
> 主要的编程方式有：
>
> 1. 命令式编程
>    - 命令“机器”如何去做事情（how），这样不管你想要的是什么（wath），它都会按照你的命令实现
>
> 2. 声明式编程
>    - 告诉“机器”你想要的是什么（what），让机器想出如何去做（how）
>    - 优点：
>      - 更加简洁、易懂，利于大型项目代码的维护
>      - 无须使用变量，避免了创建和修改状态
>
> 3. 函数式编程
> 4. 面向对象编程
>
> 命令式编程 VS 声明式编程：
>
> 例子：对一个数组的处理（即使用封装好的方法去实现）
>
> - 命令式 for
> - 声明式 map、reduce...

## 基础知识

### 1. Real DOM vs Virtual DOM

| Real DOM                  | Virtual DOM             |
| ------------------------- | ----------------------- |
| 更新缓慢                  | 更新更快                |
| 可以直接更新HTML          | 无法直接更新HTML        |
| 如果元素更新，则创建新DOM | 如果元素更新，则更新JSX |
| DOM操作代价很高           | DOM操作非常简单         |
| 消耗的内存较多            | 很少的内存消耗          |

###  2. 什么是React

- 用于构建用户界面的JavaScript库
- 声明式
  - 声明式编写UI，让代码更加可靠
- 组件化
  - 创建拥有各自状态的组件
  - 构成更加复杂的UI

### 3. React有什么特点

- 使用Virtual DOM
- 可以用服务器端渲染
- 遵循单向数据流或数据绑定

### 4. React优点

- 提高应用的性能
- JSX，代码的可读性很好

### 5. 什么是JSX

JSX（JavaScript XML），是React 使用的**一种文件**，它利用**JavaScript 的表现力和类似HTML 的模板语法**。

这使得HTML 文件非常 *容易理解*。此文件能使应用非常 *可靠*，并能够 *提高其性能*。

### 6. 了解Virtual DOM及工作原理

Virtual DOM 是一个轻量级的**JavaScript 对象**，最初只是 *Real DOM 的副本*。

它是一个**节点树**，它将 *元素*、它们的 *属性*和 *内容*作为**对象及其属性**。

React 的渲染函数从React 组件中创建一个节点树。然后它响应数据模型中的变化来更新该树，该变化是由用户或系统完成的各种动作引起的。

1. Virtual DOM 工作过程有三个简单步骤：

   - 每当底层数据发生改变时，整个UI 都将在Virtual DOM描述中重新渲染

     ![virtual-dom-step-01](img\virtual-dom-step-01.png)
   
   - 然后计算之前DOM 表示与新表示之间的差异
   
     ![virtual-dom-step-02](img\virtual-dom-step-02.png)
   
   - 完成计算后，将只有实际更改的内容更新real DOM
   
     ![virtual-dom-step-03](img\virtual-dom-step-03.png)

### 7. React ES5 VS ES6

```jsx
# 1. require 与 import
# 2. export 与 exports
# 3. component 与 function
# 4. props
# 5. state
```



``` JSX
# es5
var React = require('react');
var MyComponent = React.createClass({
    getInitialState: function() {
        return {
            lastName: 'world'
        }
    }
    propTypes: {firstName: React.PropTypes.string},
    render: function() {
        return
        <h3>{this.props.firstName} {this.state.lastName}!</h3>
    }
})
module.exports = MyComponent;
```

``` jsx
# es6
import React from 'react'; 

class MyComponent extends React.Component {
    constructor() {
        super();
        this.state = {
            lastName: 'world'
        }
    }
    
    render() {
        return
        	<h3>{this.props.firstName} {this.state.lastName}!</h3>
    }
}

export default MyComponent;
```

### 8. React vs Angular vs Vue

| 主题     | React              | Vue  | Angular      |
| -------- | ------------------ | ---- | ------------ |
| 体系结构 | 只有MVC 中的View   |      | 完整的MVC    |
| 渲染     | 可以在服务器端渲染 |      | 客户端渲染   |
| DOM      | 使用virtual DOM    |      | 使用real DOM |
| 数据绑定 | 单向数据绑定       |      | 双向数据绑定 |
| 调试     | 编译时调试         |      | 运行时调试   |

React：

推广了Virtual DOM，并创造了新的语法 —— JSX，JSX 允许在JavaScript 中写HTML

Vue:

Vue 致力解决的问题与React 一致，但却提供了另外一套解决方案。Vue 使用模板系统而不是JSX，使其对现有应用的升级更加容易



React 与 Vue 存在很多相似之处，都是JavaScript的UI 框架，专注于创造前端的富应用。

模板 vs JSX

**Vue**

鼓励写近似常规HTML的模板，写起来很接近标准HTML元素，只是多了一些属性

``` vue
<ul>
	<template v-for="item ini items">
		<li>{{item}}</li>
    </template>
</ul>
```

**React**

推荐所有的模板通用JavaScript的语法扩展——JSX

```jsx
<ul>
	{
        this.data.items.map(item => {
        	return (
                <li>{item}</li>
            )
        })
    }
</ul>
```

