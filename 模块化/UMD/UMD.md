# UMD

## 1. 什么是UMD

UMD（Universal Module Definition通用模块定义规范）是AMD + CommonJS的结合。

随着大前端的趋势所诞生，它可以通过运行时或者编译时让同一个代码模块在使用CommonJS、CMD 甚至是AMD 的项目中运行。未来同一个JavaScript 包运行在浏览器端、服务器端甚至是APP 端都只需要遵守同一个写法就行了

**代码实现：**

``` js
(function (window, factory) {
  if (typeof exports === 'object') {
    module.exports = factory();
  } else if (typeof define === 'function' && define.amd) {
    define(factory);
  } else {
    window.eventUtil = factory();
  }
});
```

不难发现，它在定义模块的时候会检测当前使用环境和模块的定义方式，将各种模块化定义方式转化为同样一种写法

## 2. demo

``` js
(function (global, factory) {
  if (typeof exports === 'object') {
    // commonJS
    var $ = require('jquery');
    module.exports = factory($);
  } else if (typeof define === 'funtion' && define.amd) {
    // AMD
    define(['jquery'], factory)
  } else {
    global.module = factory(global.Jquery);
  }
})(this, ($) => {
  //...
})
```

