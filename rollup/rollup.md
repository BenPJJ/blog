# rollup

## 概念

rollup.js 是一个js模块打包器，可以将小块代码编译成大块复杂的代码。例如Vue、React 等诸多知名框架或类库都通过rollup.js 进行打包。优点小巧而专注。

## rollup和webpack区别

- 特性

  >rollup所有资源放同一个地方，一次性加载，利用tree-shake特性来剔除未使用的代码，减少沉余
  >
  >webpack拆分代码、按需加载

- rollup

  > - 打包js文件的时候如果发现无用变量，会将其删除
  > - 可以将js编程成多种格式

- webpack

  > - 代码拆分
  >
  > - 静态资源导入（如：js、css、图片、字体等）
  >
  >   拥有如此强大的功能，所以webpack在进行资源打包的时候，就会产生很多沉余的代码

- 总结

  > 项目（特别是类库）只有js，而没有其他的静态资源文件，使用webpack就会有点大材小用了，因为webpack bundle文件的体积略大，运行略慢，可读性略低。所以，对于应用使用webpack，对于类库是使用rollup

## rollup.js的工作原理

rollup.js 可以将我们编写的JavaScript 代码（通过插件可以支持更多语言，如Typescript）与第三方模块打包在一起，形成一个文件，该文件可以是一个库（Library）或者一个应用（App），在打包过程中可以应用各类插件实现特定功能

![rollup](img\rollup.jpg)

rollup.js 默认采用ES 模块标准，可以通过`rollup-plugin-commonjs` 插件使之支持CommonJS 标准

## 安装rollup.js

> npm install rollup --global
>
> npm install rollup --save-dev

## 打包方式

- 命令行接口

  > rollup src/index.js -o dist/bundle.js -f esm
  >
  > `-f` 是`--output.format` 的缩写，指定创建的bundle 的类型，可选值值是`cjs` 、`esm` 、`system` 、`amd` 、`iife` 、`umd`

  这种方法在生成sourcemap 时灵活性不高

- 配置文件

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

  > rollup -c ./rollup.config.js
  > // rollup --config rollup.config.js

- JavaScript Api
  - rollup

    `rollup.rollup` 函数返回一个Promise，它携带了一个`bundle` 对象，此对象带有不同的属性及方法

    ``` js
    const rollup = require('rollup');
    
    rollup.rollup(config).then(bundle => bundle.generate(config.output)).then(({code}) => {})
    ```

  - bundle

    bundle对象，包含的属性和方法

    - 属性

      **imports** 一组外部依赖

      **exports** 入口点导出的名称数组

      **modules ** 模块对象数组

    - 方法

      **generate()** 模块对象数组

      **write() ** 将包写入磁盘



