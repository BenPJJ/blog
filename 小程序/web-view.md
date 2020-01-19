# web-view

承载网页的容器，会自动铺满整个小程序页面

## 支持的接口

`web-view` 网页中可使用`JSSDK 1.3.2` 提供的接口返回小程序网页

### 1. wx.miniProgram.getEnv

获取当前环境

``` js
wx.miniProgram.getEnv((res) => console.log(res.miniprogram))
```

### 2. wx.miniProgram.postMessage

向小程序发送信息，会在特定时机（小程序后退、组件销毁、分享）触发组件的`message` 事件

``` js
wx.miniProgram.postMessage({data: 'foo'})
```

### 3. wx.miniProgram.navigateTo

跳转页面

``` js
wx.miniProgram.navigateTo({url: '/path/to/page'})
```

