# React 组件

## 1. 理解“在React 中，一起都是组件”

组件是React 应用 UI 的构建块。

这些组件将整个UI 分成小的独立并可重用的部分。

每个组件彼此独立，而不会影响UI 的其余部分。

## 2. 解释React 中render()

每个React 组件强制要求必须有一个render()，它返回一个React 元素，是原生DOM 组件的表示。

## 3. props

props 是React 中属性的简写，它们是只读组件，即不可变。

它们总是在整个应用中从父组件传递到子组件，子组件永远不能将prop 送回父组件。

有助于维护单向数据流，通常用于呈现动态生成的数据。

## 4. state

状态是React 组件的核心，确定组件呈现和行为对象

## 5. Props vs State

| 条件                 | State | Props |
| -------------------- | ----- | ----- |
| 从父组件中接受初始值 | yes   | yes   |
| 父组件可以改变值     | no    | yes   |
| 在组件中设置默认值   | yes   | yes   |
| 在组件的内部变化     | yes   | no    |
| 设置子组件的初始值   | yes   | yes   |
| 在子组件的内部更改   | no    | yes   |

## 6. 区分有状态和无状态

## 7. React 组件生命周期阶段

- 初始化渲染阶段
- 更新阶段
- 卸载阶段

## 8. React 组件生命周期方法

```jsx
# 渲染之前执行
componentWillMount

# 仅在第一次渲染后执行
componentDidMount

# 当从父类接收到props，并且在调用另一个渲染器之前
componentWillReceiveProps

# 根据特定条件返回true 或 false
shouldComponentUpdate

# 在DOM 中进行渲染之前调用
componentWillUpdate

# 在渲染发生后立即调用
componentDidUpdate

# 从DOM 卸载组件后调用
componentWillUnmount
```

## 9. refs

Refs 是React 中引用的简写，它是一个有助于存储对特定的React 元素或组件的引用的属性，它将由组件

## 10. 受控组件和非受控组件