# vue-clipboard2

 一个用于剪贴板.js的简单vuejs 2绑定 

## 安装

``` shell
npm install --save vue-clipboard2
```

## 基本配置

``` js
import VueClipboard from 'vue-clipboard2';
import Vue from 'vue';

Vue.use(VueClipboard);
```

## Example

**First**

``` vue
<template>
  <div id="test">
    <input type="text" v-model="message">
    <button type="button" v-clipboard:copy="message" v-clipboard:success="onCopy" v-clipboard:error="onError">Copy!</button>
  </div>
</template>

<script>
export default {
  name: 'Test',
  data() {
    return {
      message: 'Copy These Text',
    };
  },
  methods: {
    onCopy(e) {
      alert('You just copied:' + e.text);
    },
    onError(e) {
      alert('Failed to copy texts');
    },
  },
};
</script>
```

**Second**

``` vue
<template>
  <div id="test">
    <input type="text" v-model="message">
    <button type="button" @click="doCopy">Copy!</button>
  </div>
</template>

<script>
export default {
  name: 'Test',
  data() {
    return {
      message: 'Copy These Text',
    };
  },
  methods: {
    doCopy() {
      this.$copyText(this.message).then((e) => {
        alert('Copied');
        console.log(e);
      }, (e) => {
        alert('Can not copy');
        console.log(e);
      });
    },
  },
};
</script>
```



