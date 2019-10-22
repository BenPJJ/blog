# CMD

## 1. 什么是CMD

CMD（Common Module Definition通用模块定义规范）

它是类似CommonJS 模块化规范，但是运行与浏览器之上的

CMD 推崇依赖就近，所以一般不在define 的参数中写依赖，在factory 中写

**格式如下：**

``` js
define(factory);
```

**代码实现：**

``` js
// a.js
define(function(require, exports, module) {
  module.exports = {
    a: 1;
  };
});
```

``` js
// b.js
define(function(require, exports, module) {
  var ma = require('./a.js');
  var b = ma.a + 2;
  module.exports = {
    b: b
  };
});
```

## 2. seaJS 是典型遵守CMD的JS框架

