# Vue vs React

## 数据

> 数据是不是可变的

**React**

react 整体是函数式的思想，把组件设计成纯组件，状态和逻辑通过参数传入

因此在react 中，是单向数据流

![react-life](img\react-life.webp)

**Vue**

vue 的思想是响应式的，也就是基于数据可变

通过对每个属性建立watcher 来监听，当属性变化的时候，响应式的更新对应的虚拟dom

![vue-life](img\vue-life.webp)

> 总之，react 的性能优化需要手动去做，而vue 的性能优化是自动的，但是vue 的响应式机制也有问题，就是当state 特别多的时候，Watcher 也会很多，会导致卡顿，所以大型应用（状态特别多的），一般用react，更加可控

## 写法

> 通过js 来操作一切，还是用各自的处理方式

**React**

react 的思路是all in js，通过js 来生成html、js来操作css等

**Vue**

vue 是把html、css、js 结合到一起，用各自的处理方式，vue 有单文件组件，可以把html、css、js 写到一个文件中，html 提供了模板引擎来处理

``` vue
<template>
	//...
</template>
<script>
	module.exports = {
        data() {
            return {
                // ...
            }
        }
    }
</script>
<style>
	// ...
</style>
```

## 组件

> 类式的组件写法，还是声明式的写法

**React**

react 是类式的写法，api很少

```jsx
class MyComponent extends React.Component {
    constructor(props) {
        super(props);
        
        this.state = {
            name: props.name || 'Hello world'
        }
    }
    
    render() {
        return (
        	<div>{this.state.name}</div>
        )
    }
}
MyComponent.propTyeps = {
    name: React.PropTypes.string
}
MyComponent.defaultProps = {
    name: ''
}
```

react 可以通过高阶组件（Higher Order Components -- HOC）来扩展

> react 刚开始也有mixin的写法，React.createClass

``` jsx
import React, { Component } from 'react';

export default (WrappedComponent) => {
    class NewComponent extends Componet {
        constructor() {
            super();
            this.state = {
                name: ''
            }
        }
        
        componentWillMount() {
            const name = localStorage.getItem('name');
            this.setState({ name: name })
        }
        
        render() {
            return <WrappedComponent name={this.state.name}></WrappedComponent>
        }
    }
    
    return NewComponent;
}
```

**Vue**

> vue3.0 支持类式写法

vue 是声明式的写法，通过传入各种options、api、参数。

```vue
var myComponent = Vue.extend({
	template: `<div>{{name}}</div>`,
	props: {
		name: {
			type: String,
			default: ''
		}
	}
})
```

vue 需要通过mixins 来扩展

> vue 也不是不能实现高阶组件，只是特别麻烦，需要对组件的option 做各种处理

```vue
var myMixin = {
	create: () => {
		this.hello();
	},
	methods: {
		hello: () => {
			console.log('hello world');
		}
	}
}

var MyComponent = Vue.extend({
	mixins： [myMixin]
})

var component = new MyComponent;
```

## 功能

> 什么功能内置，什么交给社区去做

