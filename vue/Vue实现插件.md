# Vue实现插件

随着项目编写的进行，代码量越来越多，重复的内容随之增加，我们可以创建一个通用的组件（全局组件），然后再每个需要的地方调用，减少代码量，简化代码结构。

## 好的库应该具备条件

- 文档要全
- eslint要做
- 需要支持esm、umd
- 版本号规范、目录规范

## 逻辑

- 创建一个空对象，这个对象就是日后要使用的插件的名字。此外，这个对象中要有一个install 的函数。
- 使用vue 的extend 方法创建一个插件的构造函数（可以看做创建一个vue 的子类），实例化该对象，之后的所有操作都可以通过这个子类完成。
- 之后再Vue 的原型上添加一个共用的方法。

## 源码

### 第一种实现方法：

``` vue
// Toast.vue
<template>
  <transition name="fade">
    <div class="toast" v-show="show">
      {{message}}
    </div>
  </transition>
</template>

<script>
export default {
  data() {
    return {
      show: false,
      message: ''
    }
  }
}
</script>

<style>
  .toast {
    position: fixed;
    top: 40%;
    left: 50%;
    margin-left: -15vw;
    padding: 2vw;
    width: 30vw;
    font-size: 4vw;
    color: #fff;
    text-align: center;
    background-color: rgba(0, 0, 0, 0.8);
    border-radius: 5vw;
    z-index: 999;
  }
  .fade-enter-active,
  .fade-leave-active {
    transition: 0.3s ease-out;
  }
  .fade-enter {
    opacity: 0;
    transform: scale(1.2);
  }
  .fade-leave-to {
    opacity: 0;
    transform: scale(0.8);
  }
</style>
```

``` js
// Toast.js
import ToastComponent from './Toast.vue';

const Toast = {};
// 注册Toast
Toast.install = function(Vue) {
  // 生成一个Vue的子类
  // 同时这个子类也就是组件
  const ToastConstructor = Vue.extend(ToastComponent);
  // 生成一个该子类的实例
  const instance = new ToastConstructor();
  // 将这个实例挂载在我创建的div上
  // 并将此div加入全局挂载点内部
  instance.$mount(document.createElement('div'));
  document.body.appendChild(instance.$el);
  // 通过Vue的原型注册一个方法
  // 让所有实例共享这个方法
  Vue.prototype.$toast = (msg, duration = 2000) => {
    instance.message = msg;
    instance.show = true;
    setTimeout(() => {
      instance.show = false;
    }, duration);
  };
};

export default Toast;
```

``` json
// package.json
{
  "name": "bz-toast",
  "version": "1.0.0",
  "description": "一个弹窗插件",
  "main": "Toast.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

### 第二种实现方法：

``` vue
// Load.vue
<template>
  <div class="wrapper" v-if="isShow">
    <div class="loading">
      <img src="./timg.gif" alt="" width="40" height="40">
    </div>
  </div>
</template>

<script>
export default {
  props: {
    isShow: {
      type: Boolean,
      default: false
    }
  }
}
</script>
```

``` js
// Load.js
import LoadingComponent from './load.vue';

let Loading = {};

Loading.install = (Vue) => {
  Vue.component('loading', LoadingComponent)
};

export default Loading;
```

``` json
// package.json
{
  "name": "bz-loading",
  "version": "1.0.0",
  "description": "一个加载登陆模块",
  "main": "load.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}

```

### 两种方法的区别

- loading 是显示的写在app.vue 模板里的，而toast并没有作为一个组件写入，仅仅是通过一个方法控制显示
- toast 插件没有在挂载点里面，而是独立存在的，也就是说当执行`vue.use(toast)` 之后，该插件就是生成好的了，之后的所有操作无非就是显示或者隐藏的问题了

## 发布npm

``` shell
cd ...
npm login
npm publish
```

## 使用插件

``` shell
npm install --save bz-toast
```

``` js
// main.js
import Toast from 'bz-toast';
Vue.use(Toast)
```

``` vue
<template>
  <div id="date">
    <button @click="toast">显示taost弹出框</button>
  </div>
</template>

<script>
export default {
  methods: {
    toast() {
      this.$toast('你好');
    }
  }
}
</script>
```

