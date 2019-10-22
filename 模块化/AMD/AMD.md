# AMD

## 1. 什么是AMD

AMD（Asynchronous Module Definition异步模块定义规范），一个在浏览器端模块化开发的规范

由于不是JavaScript 原生支持，使用AMD 规范进行页面开发需要用到对应的库函数，也就是require.js

它是依赖前置（依赖必须一开始就写好）会先尽早地执行（依赖）。换句话说，所有require 都被提前执行（require 可以是全局或局部）

AMD 是为了弥补commonjs 规范在浏览器中目前无法支持ES6 的一种解决方案。

AMD 规范只定义了一个函数`defind` ，它是全局变量

**格式如下：**

``` js
defind(id?, dependencies?, factory)
```

- **id：** 
  - 可选，用来定义模块的标识，如果没有提供该参数，脚本文件名（去掉拓展名）
- **dependencies：** 
  - 是一个当前模块依赖的模块名称数组
- **factory：** 
  - 工厂方法，模块初始化要执行的函数或对象。如果为函数，它应该只被执行一次。如果是对象，此对象应该为模块的输出值

## 2. requireJS 是典型遵守AMD的JS框架

