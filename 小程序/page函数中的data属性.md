## page函数中的data属性

`page()` 函数中的`data:{}` 属性，通常是保存页面需要绑定的数据，一般在里面，设置一个变量，用来接收从服务器加载来的`JSON` 数据，然后在通过数据绑定的方式绑定到页面上面

![data](img\data.png)

## app.js的生命周期

`app.js `是关于整个小程序项目的方法和属性，类似页面`Page({...})` 函数，也需要一个外层函数包裹`App({...})`

### onLaunch

当小程序初始化完成时，会触发`onLaunch`（全局只触发一次）

``` js
onLaunch: function () {}
```

### onShow

当小程序启动，或从后台进入前台显示，会触发`onShow`

``` js
onShow: function (options) {}
```

### onHide

当小程序从前台进入后台，会触发`onHide`

``` js
onHide: function () {}
```

### onError

当小程序发生脚本错误，或者`api` 调用失败时，会触发`onError` 并带上错误信息

``` js
onError: function (msg) {}
```

