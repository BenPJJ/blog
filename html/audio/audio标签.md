# audio标签

``` html
<audio controls="controls" src="">您的浏览器不支持audio标签</audio>
```

通常会在该标签中放置文本内容，让不支持该标签的浏览器显示文本内容，用户体验更好

**属性**

- autoplay 自动播放
- controls 显示音频控件
- loop 重复播放
- muted 静音
- preload 当网页加载时，音频是否默认被加载以及如何被加载，值 auto/metadata/none
- src 地址

## 在vue中使用

### 第一种：

将音频放置在static 目录中，然后进行调用

``` html
<div :class="['music', {'open': isOpen}]" @click="switchMusic">
  <audio autoplay="autoplay" loop="loop" controls="controls"
         preload="auto"
         src="../../static/audio/music.mp3" style="display:none" ref="mp3">
    您的浏览器不支持audio标签
  </audio>
</div>
```

### 第二种：

给项目配置mp3格式的解析器

1. 在**webpack.base.conf.js** 中添加加载器

   ``` js
    {
      test: /\.(mp4|webm|ogg|mp3|wav|flac|aac)(\?.*)?$/,
      loader: 'url-loader',
      options: {
      		limit: 10000,
         name: utils.assetsPath('audio/[name].[hash:7].[ext]')
      }
    },
   ```

2. 在**vue-loader.config.js** 文件为audio 的src 属性添加转换属性选项，让**vue-loader** 知道需要将audio 的src 属性的内容转换为模块

   ``` js
   transformToRequire: {
     "audio": "src"
   }
   ```

3.  添加audio 标签，引入资源文件

   ``` vue
   <div :class="['music', {'open': isOpen}]" @click="switchMusic">
     <audio autoplay="autoplay" loop="loop" controls="controls"
            preload="auto"
            src="../assets/audio/music.mp3" style="display:none" ref="mp3">
       您的浏览器不支持audio标签
     </audio>
   </div>
   ```

## 使用公司脚手架开发

1. 在**webpack.config.js** 中添加加载器

   ``` js
   {
     test: /\.mp3$/,
     loader: 'url-loader',
     options: {
       limit: 10000,
       name: './audio/[name].[ext]?[hash]',
     },
   },
   ```

2. 在**module =》 rules =》/\.vue$/** 下添加

   ``` js
   options: {
     transformToRequire: {
       audio: "src"
     }
   }
   ```

## 开发中遇到的问题

### 问题一：所有页面都需要音乐

``` js
// app.vue
<div :class="['music', {'open': isOpen}]" @click="switchMusic">
  <audio autoplay="autoplay" loop="loop" controls="controls"
         preload="auto"
         src="../assets/audio/music.mp3" style="display:none" ref="mp3">
    您的浏览器不支持audio标签
  </audio>
</div>
```

### 问题二：移动端 h5 ios 不能自动播放音乐

**原因：**

ios 是没办法调用`audio.play()` 事件直接调用，非得添加手动点击事件才可以

- 方法：当浏览器打开页面时，触碰屏幕触发事件，进行音频播放

  ```vue
  <template>
  	<div id="app" @touchstart.once="playMusic">
    	// ...
    </div>
  </template>
  
  <script>
  	export default {
      data() {
        return {
          isIos: /(iPhone|iPad|iPod|iOS)/i.test(navigator.userAgent),
        };
      },
      methods: {
        playMusic() {
          if (this.isIos) this.$refs.mp3.play();
        },
      },
    };
  </script>
  ```

### 问题三：ios、android 在微信中audio 不能自动播放

**原因：**

android ios 内部原因，为了节省流量，规定不自动播放音频视频

- 方法一：等待微信端页面加载完毕，触发音频播放

  ``` vue
  <script>
    export default {
      data() {
        return {};
      },
      methods: {
        play() {
          document.removeEventListener('WeixinJSBridgeReady', this.play);
          document.removeEventListener('YixinJSBridgeReady', this.play);
          this.$refs.mp3.play();
        },
      },
      mounted() {
        document.addEventListener('WeixinJSBridgeReady', this.play, false);
      	document.addEventListener('YixinJSBridgeReady', this.play, false);
      },
    };
  </script>
  ```

- 方法二：

  ``` vue
  // index.html
  <script src="https://res.wx.qq.com/open/js/jweixin-1.4.0.js"></script>
  
  <script>
  	export default {
      data() {
        return {};
      },
      methods: {
        autoPlayAudio() {
          wx.ready(() => {
            this.$refs.mp3.play();
          });
        },
      },
    };
  </script>
  ```

  

