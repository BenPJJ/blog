# React

## Reactjs

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



