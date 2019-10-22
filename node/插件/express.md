# express

## 1. 什么是Express

Express 是一个基于 Node.js 封装的上层服务框架，它提供了更简洁的 API 更实用的新功能。它通过中间件和路由让程序的组织管理变的更加容易；它提供了丰富的 HTTP 工具；它让动态视图的渲染变的更加容易；它还定义了一组可拓展标准。

## 2. 安装

``` js
npm install --save-dev express
```

## 3. 特点

- 实现了路由功能
- 中间件功能
- 扩展了req和res对象
- 可以集成其他模板引擎

## 4. 使用

``` js
// app.js
const express = require('express');
const app = express(); // 创建一个app应用
app.get('/', (req, res) => { // 注册路由（这里只能监听get方法和根目录）
	res.send('indexPage');
});
app.listen(8080, () => {
  console.log('port created successfully......');
});
```

浏览器访问根目录页面显示：indexPage

如果访问其他路径，虽然没有为其他路径设置响应内容，但是服务器并不会报错，而是在页面显示：Cannot GET /

## 5. API

### send()

- res.send() 参数类型除了能接收字符串和Buffer，还可以接收数组或者对象
- res.send() 会自动发送更多的响应报文头，例如设置content-Type为utf-8，所以中文也没有乱码

### end()

- res.end() 参数类型只能接收字符串和Buffer

### get（）

- app.get() 注册路由
- 请求方法必须是get方法，而且路径是严格匹配的（忽略url 后面拼接的参数，例如?name=123这类）

### use()

- app.use() 注册路由
- 不限定请求的方法，get/post等都可以
- 路径模糊匹配，这个路径和它路径下的子路径都可以匹配

``` js
app.use('/item', function (req, res) {
    res.send('itemPage');
})
//http://localhost:8080/item 成功
//http://localhost:8080/item/233 成功
//http://localhost:8080/item?name=hello 成功
//http://localhost:8080/123/item 失败
//http://localhost:8080/item233 失败
```

### all()

- app.all() 注册路由
- 不限定请求的方法，但是请求路径要求严格匹配

### 使用正则表达式注册路由

``` js
var reg = /^\/item(\/.+)*$/;
app.get(reg, function (req, res) {
    res.send('itemPage');
})
```

### params

通过req.params 获取路由中的参数

使用`:` 号分隔路径，这些路径将被以对象的形式保存到req.params中

``` js
app.get('/item/:year/:month/:day', function (req, res) {
    res.send(req.params);
})
```

浏览器地址栏输入：[http://localhost:8080/item/2019/5/19](https://links.jianshu.com/go?to=http%3A%2F%2Flocalhost%3A8080%2Fitem%2F2019%2F5%2F19)
返回结果：{"year":"2019","month":"5","day":"19"}

### static

通过express 模拟Apache 实现静态资源托管服务

express.static(root, [options]) 返回静态资源文件，并且会自动设置响应的文档类型

参数一：静态资源的根目录

## Express 的静态文件中间件

``` js
const express = require('express');
const path = require('path');
const app = express();
const pubilcPath = path.resolve(__dirname, 'public');
app.use(express.static(pubilcPath))
```

