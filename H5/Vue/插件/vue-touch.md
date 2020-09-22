# vue-touch

手势切换页面的功能

## 1. 安装

```js
npm install --save vue-touch@next
```

## 2. 引用文件

``` js
import VueTouch from 'vue-touch';
Vue.use(VueTouch, {name: 'v-touch'});
```

## 3. vue文件

``` html
<v-touch @swipeleft="left" @swiperight="right">
  // ...
</v-touch>
```

``` js
methods: {
  left() {
    console.log('left');
  },
  right() {
    console.log('right');
  }
}
```

