# 小程序API

## wx.getSystemInfo

获取系统信息

``` js
wx.getSystemInfo({
  success: function (res) {
    console.log(res.screenHeight)
  }
})
```

## wx.createSelectorQuery()

返回一个SelectorQuery 对象实例

``` js
const query = wx.createSelectorQuery() // 创建节点查询器 query
query.select('#group').boundingClientRect() // 这段代码的意思是选择ID=group 的节点，获取节点位置信息的查询请求
query.selectViewport().scrollOffset() // 这段代码的意思是获取页面滑动位置的查询请求
query.exec(function (data) {
  data[0].top // #group 节点的上边界坐标
  data[1].scrollTop // 显示区域的竖直滚动位置
})
```

## wx.getUserInfo()

获取用户信息

``` html

```

## wx.showShareMenu()

显示当前页面的转发按钮

