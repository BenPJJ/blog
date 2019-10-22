# vue-lazyload

## 1. 安装

``` js
npm install --save vue-lazyload
```

## 2. 引入文件

一般在main.js 全局引入，且配置好图片

``` js
// main.js
import Vue from 'vue';
import VueLazyload from 'vue-lazyload';

Vue.use(VueLazyload);
// or with options
Vue.use(VueLazyload, {
  preLoad: 1.3,
  error: 'dist/error.png',
  loading: 'dist/loading.gif',
  attempt: 1
})
```

## 3. vue文件中使用

将需要懒加载的图片绑定v-bind:src 修改为v-lazy

``` html
<ul>
  <li v-for="img in list">
  	<img v-lazy="img.src">
  </li>
</ul>
```

