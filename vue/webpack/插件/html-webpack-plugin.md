# html-webpack-plugin

- 直接为项目生成一个或多个HTML文件（HTML文件个数由插件实例的个数决定），并将webpack打包后输出的所有脚本文件自动添加到插件生成的HTML文件中
- 通过配置，可以将根目录下用户自定义的HTML文件作为插件生成HTML文件的模板
- 通过向插件传递参数，控制HTML文件的输出

## 安装

``` shell
npm install html-webpack-plugin --save-dev
```

## 基本配置

``` js
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
  // ...
	plugins: [
    new HtmlWebpackPlugin({
      bzConfigPath: '/common/js/config.js',
    })
  ]
  // ...
}
```

``` html
<script src="<%=htmlWebpackPlugin.options.bzConfigPath%>"></script>
```

