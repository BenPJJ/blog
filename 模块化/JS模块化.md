# JS模块化

## 1. js模块化类型

### CommonJS

[CommonJS](./commonJS/commonJS.md)

### AMD和requireJS

[AMD](./AMD/AMD.md)

[requireJS](./requireJS/requireJS.md)

### CMD和seaJS

[CMD](./CMD/CMD.md)

[seaJS](./seaJS/seaJS.md)

### ES6 Module

[ES6 Module](./ES6 Module/ES6 Module.md)

### UMD

[UMD](./UMD/UMD.md)

## 2. AMD和CMD的区别

AMD 推崇依赖前置、提前执行，CMD 推崇依赖就近、延迟执行

``` js
// AMD写法
define(['a', 'b'], function(a, b) {
  // 等于在前面声明并初始化了要用到的所有模块
  a.doSomething();
  if(false) {
    // 即便没用某个模块b，但b还是提前执行了
    b.doSomething();
  }
})
```

``` js
// CMD写法
define(function(require, exports, module) {
  var a = rquire('./a'); // 在需要时申明
  a.doSomething();
  if (false) {
    var b = require('./b');
 		b.doSomething();
  }
})
```

``` js
// require.js
// 定义模块main.js
define(['main', 'jquery'], funtion($) {
 var add = function(a, b) {
  	return a + b;
  }
	return {
  	add: add
  }    
})
// 加载模块
require(['main'], function(math) {
  math.add();
})
```

``` js
// sea.js
// 定义模块main.js
define(function(require, exports, module) {
  var $ = require('jquery.js');
  var add = function(a, b) {
    return a + b;
  }
  exports.add = add;
})
// 加载模块
seajs.use(['main.js'], function(math) {
  var sum = math.add(1 + 2);
})
```

## 3. CommonJS和ES6 Module的区别

### CommonJS模块输出的是一个值的拷贝，ES6模块输出的是值的引用

- CommonJS 模块输出的是值的拷贝，也就是说，一旦输出一个值，模块内部的变化就影响不到这个值
- ES6 模块的运行机制与CommonJS 不一样。JS 引擎对脚本静态分析的时候，遇到模块加载命令`import` ，就会生成一个只读引用。等到脚本真正执行时，在根据这个只读引用，到被加载的那个模块里面去取值。换句话说，ES6 的`import` 有点像 Unix 系统的“符号连接”，原始值变了，`import`加载的值也会跟着变。因此，ES6 模块是动态引用，并且不会缓存值，模块里面的变量绑定其所在的模块。

### CommonJS模块是运行时加载，ES6模块是编译时输出接口

- 运行时加载：CommonJS 模块就是对象，即在输入时是先加载整个模块，生成一个对象，然后再从这个对象上面读取方法，这个加载称为“运行时加载”
- 编译时加载: ES6 模块不是对象，而是通过 `export` 命令显式指定输出的代码，`import`时采用静态命令的形式。即在`import`时可以指定加载某个输出值，而不是加载整个模块，这种加载称为“编译时加载”。