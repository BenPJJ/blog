# React

## Reactjs

### 工具

#### react-app-rewired

![react-app-rewired](img\react-app-rewired.png)

- config-overrides.js 剖析

  ``` jsx
  ![react-app-rewired](D:\blog\React\img\react-app-rewired.png)module.exports = function overrides(config, env) {
    ...
    return config;
  }

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
    
	// env
	development
  ```

