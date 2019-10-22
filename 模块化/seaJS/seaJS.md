# seaJS

## 1. 什么是seaJS

seaJS 是用JavaScript 编写的JS 框架

**主要功能是** 可以按不同的先后依赖关系对JavaScript 等文件的进行加载工作，可简单理解为JS 文件的加载器，它非常适合在浏览器中使用，它可以确保所依赖的JS 文件加载完成之后再加载当前的JS 文件，这在大量使用JS 文件的项目中可确保各个JS 文件的先后加载顺序，确保避免了以前因某些原因某个文件加载慢而导致其它加载快的文件需要依赖其某些功能而出现某函数或某变量找不到的问题。

## 2. 常用接口

### config

用来对seaJS 进行配置

> seajs.config({...})

``` js
// seajs-config.js
seajs.config({
  // 两种写法：一个是paths，一个是base
  /**paths: {
    baseUrl: '.'
  },
  alias: {
    'a': 'a.js',
    'b': 'b.js'
  }*/
  base: './',
  alias: {
    'a': 'a.js',
    'b': 'b.js'
  }
})
```

``` html
// index.html
<script src="./sea.js"></script>
<script src="./seajs-config.js"></script>
<script>
	seajs.use(['a', 'b']);
</script>
```

#### base

base 是sea.js 的基本路径，也就是sea.js 的路径

#### paths

paths 当目录比较深，或需要跨目录调用模块时，可以使用paths来简化书写

### use

用来在页面中加载一个或多个模块

> seajs.use(['a','b'], function(a, b) {...})

``` html
// index.html
<script>
	seajs.use(['./a.js', './b.js']); // 没有使用别名的写法
  seajs.use(['a', 'b']); // 使用base 路径的写法
</script>
```

### define

用来定义一个模块，seaJS 推崇一个模块一个文件，遵循统一的写法

> define(function(require, exports, module) {...})

``` js
// a.js
define(function() {
  alert('aaa')
});
```

``` js
// b.js
define(function() {
  alert('bbb');
});
```

``` html
// index.html
<script>
	seajs.use(['./a.js', './b.js']);
</script>
```

#### require

require 用来获取指定模块的接口

> require(function(require){var a = require('xModule'); ...})

``` js
// seajs-config.js
seajs.config({
  paths: {
    'jquery': 'https://scdn.bozhong.com/source/moe/jquery'
  }
});
```

``` js
// index.js
define(function(require) {
  let $ = require('jquery/1.8.3/jquery-debug.js');
  console.log($);
});
```

``` html
// index.html
<script>
	seajs.use(['./index.js']);
</script>
```

#### require.async

用来在模块内部异步加载一个或多个模块

``` js
define(function(require) {
  require.async(['aModule', 'bModule'], function(a, b) {
    a.func();
    b.func();
  });
});
```

#### exports

用来在模块内部对为提供接口

``` js
// index.js
define(function(require, exports) {
  let $ = require('jquery/1.8.3/jquery-debug.js');
  $('h2').text('我改变了文本内容!');
  exports.msg = '我是对外接口';
})
```

``` html
// index.html
<script>
	seajs.use(['./index.js'], function(ms) {
    alert(ms.msg);
  });
</script>
```

#### module.exports

与exports 类似，用来在模块内部对外提供接口

``` js
define(function(require, exports, module) {
  module.exports = {
    name: 'a',
    doSomething: function() {...}
  };
})
```

## 3. demo

``` js
// a.js
define(function(require, exports, module) {
  var name = 'Jack';
  function printName() {
    console.log(name);
  }
  module.exports = {
    printName: printName
  };
});
```

``` html
<script src="./sea.js"></script>
<script>
	seajs.use('./a.js', function(a) {
    a.printName();         
  });
</script>
```

