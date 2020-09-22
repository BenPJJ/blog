# vue 优化及小技巧
---

### - 巧用Mixins
多个组件都用到一个或多个方法，可以将这些方法封装在一个js文件中

### - Object.freeze方法
- 这个方法有什么用？
  - 它主要是可以将一个对象冻结，防止对象被修改
- vue项目使用有什么优化作用？
  - vue采用了**数据劫持**的方式遍历数据对象，把这些属性转为getter、setter方法来监听并通知数据的变化，所以当遇到一个巨大的数组或者对象，并且确定数据不会修改，这是就可以使用`Object.freeze()`方法来组织vue对这个巨大数据的转化
  ```js
  new Vue({
    data: {
        // vue不会对list里的object做getter、setter绑定
        list: Object.freeze([
            { value: 1 },
            { value: 2 }
        ])
    },
    mounted () {
        // 界面不会有响应
        this.list[0].value = 100;

        // 下面两种做法，界面都会响应
        this.list = [
            { value: 100 },
            { value: 200 }
        ];
        this.list = Object.freeze([
            { value: 100 },
            { value: 200 }
        ]);
    }
  })
  ```

### - 自动化导入模块
当我们某个组件或js文件需要多个引入模块时，一般的做法就是，import每个模块，这样显然是相当繁琐的，这时`require.context`函数将派上用场

- eg: 动态生成modules对象

``` js
import { basename, dirname } from 'path';

const files = require.context('./', true, /\.js$/);
let modules = {};
let keyName = {};
files.keys().forEach(key => {
  const name = basename(key, '.js');
  const dirName = dirname(key).replace('.', '').replace('/', '');
  if (name == 'index') return;

  if (modules.hasOwnProperty(dirName)) {
    keyName[name] = files(key).default || files(key);
    let obj = modules[dirName];
    modules[dirName] = keyName;
    modules[dirName] = Object.assign(modules[dirName], obj);
    keyName = {};
  } else {
    keyName[name] = files(key).default || files(key);
    modules[dirName] = keyName;
    keyName = {};
  }
});

export default modules;
```

### - cdn引入（优化）
对于一些不常改动的模块库，例如：`vue`、`vueRouter`、`vuex`、`echarts`、`element-ui`等，我们让`webpack`不将它们进行打包，而是通过`cdn`引入，这样就可以**减少代码大小，减少服务器带宽，并通过cdn将它们缓存起来，提高网站性能**

- 通过externals加载外部CDN资源
  - 默认情况下，通过import语法导入的第三方依赖包，最终会被打包合并到同一个文件中，从而导致打包成功后，单文件体积过大的问题

    为了解决上述问题，可以通过webpack的externals节点，来配置并加载外部的CDN资源。凡是声明在externals中的第三方依赖包，都不会被打包

  ``` js
  const cdn = {
    css: [],
    js: [
      'https://unpkg.com/vue/2.5.22/vue.min.js'
    ]
  }

  moudle.exports = {
    ...
    externals: {
      'vue': 'Vue'
    },
    plugins: {
      new htmlWebpackPlugin({
        cdn
      })
    }
  }
  ```
  ``` html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="utf-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width,initial-scale=1.0">
      <link rel="icon" href="<%= BASE_URL %>favicon.ico">
      <% if (process.env.NODE_ENV === 'production') { %>
      	<!-- 引入样式 -->
        <% for(var css of htmlWebpackPlugin.options.cdn.css) { %>
          <link rel="stylesheet" href="<%=css%>">
        <% } %>
        <!-- 引入js -->
        <% for(var js of htmlWebpackPlugin.options.cdn.js) { %>
          <script src="<%=js%>"></script>
        <% } %>
      <% } %>
      <title>vue-admin-webapp</title>
    </head>
    <body>
      <noscript>
        <strong>We're sorry but vue-admin-webapp doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
      </noscript>
      <div id="app"></div>
      <!-- built files will be auto injected -->
    </body>
  </html>
  ```

  ### - 生成打包报告（优化）
  使用`webpack-bundle-analyzer`插件，生成打包报告，根据报告优化项目
