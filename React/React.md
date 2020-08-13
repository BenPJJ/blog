# React

## ReactJS

### 高阶组件

- React.Memo()

  ``` jsx
  function MyComponent(props) {
  	// 使用props渲染  
  }
  
  function areEqual(prevProps, nextProps) {
    // 如果把nextProps传入render方法的返回结果与将prevProps传入render方法的返回结果一致则返回true，否则返回false
  }
  
  export default React.memo(MyComponent, areEqual)
  ```

  当父组件引入子组件的情况下，往往会造成组件之间的一些不必要的浪费。如下面例子，每次父组件更新count，子组件都会更新，使用memo之后，count变化子组件就没有更新啦

  ``` jsx
  import React, { useState, memo } from 'react';
  
  const Child = (props) => {
    console.log('子组件')
    return (
      <div>我是一个子组件</div>
    )
  }
  
  const ChildMemo = memo(Child)
  
  function Index() {
    const [ count, setCount ] = useState(0);
  
    return (
      <div>
        <p>count:{count}</p>
        <button onClick={() => {setCount(count + 1)}}>加一</button>
        <ChildMemo />
      </div>
    )
  }
  
  export default Index;
  ```

### API

- Context

  // 使用前

  ```jsx
  import React, { Component } from 'react';
  
  class Index extends Component {
    render() { 
      return ( 
        <Toolabr theme="yellow" />
       );
    }
  }
  
  function Toolabr(props) {
    return (
      <div>
        <ThemedButton theme={props.theme} />
      </div>
    )
  }
  
  class ThemedButton extends Component {
    render() {
      return ( 
        <button style={{background: this.props.theme}}>你好</button>
       );
    }
  }
  
  export default Index;
  ```

  //  使用后

  ``` jsx
  import React, { Component, createContext } from 'react';
  
  const ThemeContext = createContext('yellow');
  
  class Index extends Component {
    render() { 
      return ( 
        // 使用一个Provider来将当前的theme传递给以下的组件树
        // 无论多深，任何组件都能读取这个值
        <ThemeContext.Provider value="blue">
          <Toolabr/>
        </ThemeContext.Provider>
       );
    }
  }
  
  function Toolabr() {
    return (
      <div>
        <ThemedButton />
      </div>
    )
  }
  
  class ThemedButton extends Component {
    // 指定contextType读取当前的theme context
  	// React 会往上找到最近的theme Provider，然后使用它的值
    static contextType = ThemeContext;
    
    render() {
      return ( 
        <button style={{background: this.context}}>你好</button>
       );
    }
  }
  
  export default Index;
  ```

  



### 工具

#### react-app-rewired

![react-app-rewired](img\react-app-rewired.png)

- config-overrides.js 剖析

  ``` js
  module.exports = function overrides(config, env) {
    ...
    return config;
  }
  ```

  ``` js
  // config
  { mode: 'development',
    bail: false,
    devtool: 'cheap-module-source-map',
    entry:
     [ 'D:\\local.project\\dome02\\node_modules\\react-dev-utils\\webpackHotDevClient.js',
       'D:\\local.project\\dome02\\src\\index.js' ],
    output:
     { path: undefined,
       pathinfo: true,
       filename: 'static/js/bundle.js',
       futureEmitAssets: true,
       chunkFilename: 'static/js/[name].chunk.js',
       publicPath: '/',
       devtoolModuleFilenameTemplate: [Function],
       jsonpFunction: 'webpackJsonpreact-template',
       globalObject: 'this' },
    optimization:
     { minimize: false,
       minimizer: [ [TerserPlugin], [OptimizeCssAssetsWebpackPlugin] ],
       splitChunks: { chunks: 'all', name: false },
       runtimeChunk: { name: [Function: name] } },
    resolve:
     { modules:
        [ 'node_modules', 'D:\\local.project\\dome02\\node_modules' ],
       extensions:
        [ '.web.mjs', '.mjs', '.web.js', '.js', '.json', '.web.jsx', '.jsx' ],
       alias: { 'react-native': 'react-native-web' },
       plugins: [ [Object], [ModuleScopePlugin] ] },
    resolveLoader: { plugins: [ [Object] ] },
    module:
     { strictExportPresence: true,
       rules: [ [Object], [Object], [Object] ] },
    plugins:
     [ HtmlWebpackPlugin {
         options: [Object],
         childCompilerHash: undefined,
         childCompilationOutputName: undefined,
         assetJson: undefined,
         hash: undefined,
         version: 4 },
       InterpolateHtmlPlugin { htmlWebpackPlugin: [Function], replacements: [Object] },
       ModuleNotFoundPlugin {
         appPath: 'D:\\local.project\\dome02',
         yarnLockFile: undefined,
         useYarnCommand: [Function: bound useYarnCommand],
         getRelativePath: [Function: bound getRelativePath],
         prettierError: [Function: bound prettierError] },
       DefinePlugin { definitions: [Object] },
       HotModuleReplacementPlugin {
         options: {},
         multiStep: undefined,
         fullBuildTimeout: 200,
         requestTimeout: 10000 },
       CaseSensitivePathsPlugin {
         options: {},
         logger: [Console],
         pathCache: {},
         fsOperations: 0,
         primed: false },
       WatchMissingNodeModulesPlugin { nodeModulesPath: 'D:\\local.project\\dome02\\node_modules' },
       ManifestPlugin { opts: [Object] },
       IgnorePlugin {
         options: [Object],
         checkIgnore: [Function: bound checkIgnore] } ],
    node:
     { module: 'empty',
       dgram: 'empty',
       dns: 'mock',
       fs: 'empty',
       http2: 'empty',
       net: 'empty',
       tls: 'empty',
       child_process: 'empty' },
    performance: false }
  ```

  ``` js
  // env
  development
  ```

  ``` js
  // config.module.rules
  [ { parser: { requireEnsure: false } },
   { test: /\.(js|mjs|jsx|ts|tsx)$/,
    enforce: 'pre',
    use: [ [Object] ],
    include: 'D:\\local.project\\dome02\\src' },
   { oneOf:
    [ [Object],
     [Object],
     [Object],
     [Object],
     [Object],
     [Object],
     [Object],
     [Object] ] } ]
  ```

  ``` js
  // rules[2].oneOf
  [ { test: [ /\.bmp$/, /\.gif$/, /\.jpe?g$/, /\.png$/ ],
     loader:
     'D:\\local.project\\dome02\\node_modules\\url-loader\\dist\\cjs.js',
     options: { limit: 10000, name: 'static/media/[name].[hash:8].[ext]' } },
   { test: /\.(js|mjs|jsx|ts|tsx)$/,
    include: 'D:\\local.project\\dome02\\src',
    loader:
    'D:\\local.project\\dome02\\node_modules\\babel-loader\\lib\\index.js',
    options:
    { customize:
     'D:\\local.project\\dome02\\node_modules\\babel-preset-react-app\\webpack-overrides.js',
     babelrc: false,
     configFile: false,
     presets: [Array],
     cacheIdentifier:
     'development:babel-plugin-named-asset-import@0.3.6:babel-preset-react-app@9.1.2:react-dev-utils@10.2.1:react-scripts@3.4.1',
     plugins: [Array],
     cacheDirectory: true,
     cacheCompression: false,
     compact: false } },
   { test: /\.(js|mjs)$/,
    exclude: /@babel(?:\/|\\{1,2})runtime/,
    loader:
    'D:\\local.project\\dome02\\node_modules\\babel-loader\\lib\\index.js',
    options:
    { babelrc: false,
     configFile: false,
     compact: false,
     presets: [Array],
     cacheDirectory: true,
     cacheCompression: false,
     cacheIdentifier:
     'development:babel-plugin-named-asset-import@0.3.6:babel-preset-react-app@9.1.2:react-dev-utils@10.2.1:react-scripts@3.4.1',
     sourceMaps: true,
     inputSourceMap: true } },
   { test: /\.css$/,
    exclude: /\.module\.css$/,
    use:
    [ 'D:\\local.project\\dome02\\node_modules\\style-loader\\index.js',
     [Object],
     [Object] ],
    sideEffects: true },
   { test: /\.module\.css$/,
    use:
    [ 'D:\\local.project\\dome02\\node_modules\\style-loader\\index.js',
     [Object],
     [Object] ] },
   { test: /\.(scss|sass)$/,
    exclude: /\.module\.(scss|sass)$/,
    use:
    [ 'D:\\local.project\\dome02\\node_modules\\style-loader\\index.js',
     [Object],
     [Object],
     [Object],
     [Object] ],
    sideEffects: true },
   { test: /\.module\.(scss|sass)$/,
    use:
    [ 'D:\\local.project\\dome02\\node_modules\\style-loader\\index.js',
     [Object],
     [Object],
     [Object],
     [Object] ] },
   { loader:
    'D:\\local.project\\dome02\\node_modules\\file-loader\\dist\\cjs.js',
    exclude: [ /\.(js|mjs|jsx|ts|tsx)$/, /\.html$/, /\.json$/ ],
    options: { name: 'static/media/[name].[hash:8].[ext]' } } ]
  ```

### 配置config-overrides.js

``` js
const path = require('path');

const resolve = (dir) => {
  return path.resolve(__dirname, '.', dir);
}

module.exports = function override(config, env) {

  config.output.publicPath = '';
  
  // 配置规则
  config.module.rules[2].oneOf.unshift({
  // const length = config.module.rules[2].oneOf.length;
  // config.module.rules[2].oneOf.splice(length - 1, 0, {
    test: /\.less$/,
    use: [ 'style-loader', 'css-loader', {
      loader: 'less-loader',
      options: {}
    } ]
  });
  
  // 配置别名
  config.resolve.alias = {
    ...config.resolve.alias,
    '@api': resolve('src/api'),
    '@page': resolve('src/Pages'),
    '@assets': resolve('src/assets'),
    '@components': resolve('src/components')
  }

  // 预览webpack配置
  fs.writeFileSync('webpack.config.json', JSON.stringify(config, (k, v) => {
    if (v instanceof RegExp) return v.toString();
    return v;
  }, '\t'), 'utf8');

  return config;
}
```

## React Hooks

``` jsx

```

### useContext

- 父子组件同一个目录

  > 这个用法存在一个问题，父子组件不在同一个目录中，如何共享AppContext这个context实例

  ``` jsx
  // Test.jsx
  import React, { useContext } from 'react';
  
  const test = () => {
  	const AppContext = React.CreateContext({});
  
  	const A = () => {
      const { name } = useContext(AppContext)
  		return (
  			<p>name:{{name}}</p>
  		)
  	}
    
    return (
      <AppContext.Provider value={{name: 'test'}}>			
      	<A/>
      </AppContext.Provider>
    )
  }
  
  export default test;
  ```

- 父子组件不在同一个目录

  > 通过Context Manager统一管理上下文的实例

  ``` jsx
  // context-manager.js
  import React from 'react';
  const AppContext = React.createContext();
  export default AppContext;
  ```

  ``` jsx
  // A.jsx
  import React, { useContext } from 'react';
  import AppContext from './context-manager';
  
  const A = () => {
    const { name } = useContext(AppContext);
    return (
      <p>name:{name}</p>
    )
  }
  
  export default A;
  ```

  ``` jsx
  // Test.jsx
  import React, { useContext } from 'react';
  import AppContext from './context-manager';
  import A from './A';
  
  const test = () => {
    return (
      <AppContext.Provider value={{name: 'pjj'}}>			
      	<A/>
      </AppContext.Provider>
    )
  }
  
  export default test;
  ```

  