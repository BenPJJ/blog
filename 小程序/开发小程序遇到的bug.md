# 开发小程序遇到的bug
---

### - 【问题】：
小程序scroll-view在安卓机上出现横向滚动条

【解决】

在代码样式中加上

``` css
::-webkit-scrollbar {
  width: 0;
  height: 0;
  color: transparent;
  display: none;
}
```

### - 【问题】：

首页是导航页，进入主页的时候，在主页手机左侧向右滑动的时候，会回到导航页

【解决】

可以把跳转方式`wx.navigateTo` 改成`wx.redirectTo`

``` js
wx.redirectTo({
  url: `../home/home?id=${id}`,
});
```

### - 【问题】 ：

通过点击按钮授权和通过`wx.getSetting接口` 获取的用户信息是不一致的，这就会导致通过按钮调用授权模块可以更改的名字无法实时传送到页面

【解决】

```js
getUserinfo: function (e) {
  const id = e.currentTarget.dataset.id;
  const userInfo = e.detail.userInfo;
  if (userInfo != undefined) {
    wx.getUserInfo({
      success (res) {
        wx.setStorageSync('userInfo', res.userInfo);
      },
      complete () {
        wx.redirectTo({
          url: `../home/home?id=${id}`,
        });
      }
    })
  } else {
    wx.showModal({
      title: '提示',
      content: '尚未进行授权，如不授权将无法使用部分功能',
      showCancel: false
    });
  }
}
```

### - 【问题】：

小程序引用服务器上的一张图片，服务器更换了图片，但是没有更换图片名称，现在小程序一直显示旧图

【解决】

小程序那边相同路径不会重新拉取，需要跟换图片的时候，可以在图片的后面加上**01、02等类似的**


### - 【问题】：

小程序向下拖拽，需要小程序的窗口底色和小程序自定义的导航栏颜色一样

<img src="img\效果图01.jpg" alt="效果图01" style="zoom:25%;" />

【解决】

在`app.json` 配置属性（或在相应的页面配置）：

``` json
{
  "window": {
    "backgroundColor": "#FF8A71", // 窗口的背景色
    "backgroundColorTop": "#FF8A71", // 顶部窗口的背景色，仅 iOS 支持
    "backgroundColorBottom": "#fff" // 底部窗口的背景色，仅 iOS 支持
  }
}
```

### - 【问题】：
渲染层网络层错误
