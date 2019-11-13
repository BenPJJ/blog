# friendly-errors-webpack-plugin

Friendly-errors-webpack-plugin 识别某些类别的webpack 错误，并清理，聚合和优先级，以提供更好的开发人员体验

## 安装

``` shell
npm install --save-dev friendly-errors-webpack-plugin
```

## 基本配置

``` js
const FriendlyErrorsPlugin = require('friendly-errors-webpack-plugin');
module.exports = {
  // ...
  plugins: [
  	new FriendlyErrorsPlugin()
  ]
  //...
}
```

## 选项

``` js
new FriendlyErrorsPlugin({
  // 运行成功
  compilationSuccessInfo: {
    message: [`Your application is running here: http://locallhost:3000`],
  },
  // 运行错误
  onErrors: ...
})
```

