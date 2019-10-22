# ES6 Module

## 1. 什么是ES6 Module

ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，旨在成为浏览器和服务器通用的模块解决方案。

ES6 的模块不是对象，`import` 命令会被JavaScript 引擎静态分析，在编译时就引入模块代码，而不是在代码运行时加载，所以无法实现条件加载

## 2. Api

### export

用于规定模块的对外接口

### import

用于输入其他模块提供的功能

## 3. demo

``` js
// main.js
// 定义模块
var basicNum = 0;
var add = function(a, b) {
  return a + b;
}
// export {basicNum, add};
export default {basicNum, add};
```

``` js
// 引入模块
// import {basicNum, add} from './b';
import b from './b';
function test(ele) {
  // ele.textContent = add(99 + basicNum);
  ele.textContent = b.add(99 + b.basicNum);
}
```

