# requireJS

## 1. 作用

**主要解决两个问题：**

- 多个js 文件可能有依赖关系，被依赖的文件需要早于依赖它的文件加载到浏览器
- js 加载的时候浏览器会停止页面渲染，加载文件越多，页面失去响应时间越长

## 2. Api

### config

指定引用路径

``` js
// requireJS-config.js
require.config({
  baseUrl: "js/lib",
  paths: {
  	'a': 'a'
  }
});
```

### define

定义模块

``` js
define(['a'], function() {
  'use strict';
  var name = 'jack';
  function printName() {
    console.log(name);
  }
  return {
    printName: printName
  }
})
```

### require

加载模块

``` js
require(['c'], function(ms) {
  ms.printName();
})
```

## 3. demo

``` js
// a.js
define('a', function() {
  var name = 'jack';
  function printName() {
    console.log(name);
  }
  return {
    printName: printName
  };
});
```

``` html
<script src="./require.js"></script>
<script>
	require(['a'], function(a) {
    a.printName();
  });
</script>
```

