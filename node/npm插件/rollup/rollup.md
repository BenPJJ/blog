# rollup

## 1. 什么是rollup

rollup.js 是JavaScript 的ES 模块打包器，例如Vue、React 等诸多知名框架或类库都通过rollup.js 进行打包。与Webpack 偏向于应用打包的定位不同，rollup.js 更专注于JavaScript 类库打包

## 2. rollup.js的工作原理

rollup.js 可以将我们编写的JavaScript 代码（通过插件可以支持更多语言，如Typescript）与第三方模块打包在一起，形成一个文件，该文件可以是一个库（Library）或者一个应用（App），在打包过程中可以应用各类插件实现特定功能

![rollup](img\rollup.jpg)

rollup.js 默认采用ES 模块标准，可以通过`rollup-plugin-commonjs` 插件使之支持CommonJS 标准

## 3. 安装rollup.js

**全局安装rollup.js**

``` shell
npm install --global rollup
```

## 4. 打包方式

### 命令行接口

``` js
rollup src/index.js -o dist/bundle.js -f esm
```

`-f` 是`--output.format` 的缩写，指定创建的bundle 的类型，可选值值是`cjs` 、`esm` 、`system` 、`amd` 、`iife` 、`umd`

这种方法在生成sourcemap 时灵活性不高

### 配置文件

创建一个`rollup.config.js` 的文件

``` js
export default {
  input: 'src/index.js',
  output: {
    file: 'dist/bundle.js',
    format: 'esm'
  }
}
```

使用配置文件的方式，如果配置文件`rollup.config.js` 和`package.json` 在同一层级，那么rollup 会自动使用配置文件，可以不用写配置文件的名字

```  js
rollup -c ./rollup.config.js
// rollup --config rollup.config.js
```

### JavaScript Api

#### rollup

`rollup.rollup` 函数返回一个Promise，它携带了一个`bundle` 对象，此对象带有不同的属性及方法

``` js
const rollup = require('rollup');

rollup.rollup(config).then(bundle => bundle.generate(config.output)).then(({code}) => {})
```

#### bundle

bundle对象，包含的属性和方法

##### 属性

**imports**

一组外部依赖

**exports**

入口点导出的名称数组

**modules**

模块对象数组

##### 方法

**generate()**

生成代码和源映射

**write()**

或将包写入磁盘

## 5. rollup和其他工具集成

### rollup-plugin-node-resolve

rollup 不能直接处理依赖，需要`rollup-plugin-node-resolve` 插件

### rollup-plugin-commonjs

rollup 可以直接处理esmodule 格式，commonjs格式，需要`rollup-plugin-commonjs` 插件，将commonjs 转成es2015

### rollup-plugin-buble

编译ES6+ 语法为ES2015，无需配置，比babel 更轻量

``` js
import resolve from 'rollup-plugin-node-resolve';
import commonjs from 'rollup-plugin-commonjs';
import buble from 'rollup-plugin-buble';

export default {
  input: './src/index.js',
  output: {
    file: './dist/bundle.js',
    format: 'cjs'
  },
  plugins: [
    resolve(),
    commonjs(),
    buble()
  ]
}
```

##  6. demo

``` js
// src/a.js
const a = 1;
export default a;
```

``` js
// src/main.js
import a from './a.js';
export default function() {
  console.log(a);
}
```