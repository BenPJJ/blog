# commonJS

## 1. 什么是CommonJS

Node.js 是commonJS 规范的主要实践者

一个单独的文件就是一个模块。每一个模块都是一个单独的作用域，也就是说，在该模块内部定义的变量，无法被其他模块读取，除非定义为global 对象的属性

commonJS 用同步的方式加载模块，在服务端，模块文件都存在本地磁盘，读取非常快，所以这样做不会有问题，但是在浏览器端，限于网络原因，更合理的方案是使用异步加载

## 2. Api

### require

读取一个文件并执行，返回文件内部的module.exports 对象

### exports

模块输出，单个输出

### module

把模块希望输出的内容放入该对象

### global

## 3. 弊端

- require 是同步的，模块系统需要同步读取模块文件内容，并编译执行以得到模块接口
- 在服务器端实现很简单，在浏览器端实现问题很多
- 浏览器端，加载JavaScript 最佳、最容易的方式是在document中插入script 标签。但是脚本标签天生异步，传统CommonJS 模块在浏览器环境中无法正常加载

## 4. demo

``` js
// a.js
// 定义模块
var name = 'Jack';
function printName() {
  console.log(name);
}
function printFullName(firstName) {
  console.log(firstName + name);
}
module.exports = {
  printName: printName,
  printFullName: printFullName
}
```

``` js
// b.js
// 加载模块
var nameModule = require('./a.js');
nameModule.printName();
```