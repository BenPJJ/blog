# Vuex
---

### - Vuex是什么
Vuex是状态管理器，用来管理Vue的所有**组件**状态

### - 为什么使用Vuex
当你打算开发大型单页应用（SPA），会出现多个视图组件依赖同一个状态，来自不同视图的行为需要变更一个状态

遇到以上情况时候，就应该考虑使用Vuex，它能把组件的共享状态抽取出来，当做一个**全局单例模式进行管理**，这样不管在何处改变状态，都会通知使用该组件做出相应修改

### - Vuex和axios捆绑
如果项目中需要使用到Vuex，为了思想统一，需要把接口写入到`actions`中，Vuex集中管理数据

![Vuex理念](https://vuex.vuejs.org/vuex.png)

+ Vuex结构：
  + modules
    + home
      - actions.js
      - getters.js
      - index.js
      - mutations.js
    + ...
  + actions.js
  + api.js
  + getters.js
  + index.js
  + mutations.js

- eg: 动态生成modules对象
  ``` js
  // index.js
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

### - 简单讲解Vuex

---
> 参考文献：inside.seedit.com/activity/ivf
