# webpack-bundle-analyzer

webpack 打包体积优化

## 安装

``` js
npm install --save-dev webpack-bundle-analyzer
```

## 基本配置

``` js
const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin;
module.exports = {
  // ...
	plugins: [
    new BundleAnalyzerPlugin()
  ]
  // ...
}
```

