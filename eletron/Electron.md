# Electron

## 简介

使用 JavaScript，HTML 和 CSS 构建跨平台的桌面应用程序

## 使用

1. 新建一个目录，初始化npm

   ``` shell
   mkdir HW
   cd HW
   npm init
   ```

2. 修改package.json

   ``` json
   {
     "name": "BZ",
     "version": "1.0.0",
     "description": "",
     "main": "main.js",
     "scripts": {
       "start": "electron ."
     },
     "author": "",
     "license": "ISC",
     "devDependencies": {
       "electron": "^10.1.3"
     }
   }
   ```

3. 安装electron

   ``` shell
   npm install electron --save-dev
   ```

   因为被墙的原因，通常都是安装失败（read ECONNRESET），通过单独配置electron的淘宝源来下载安装

   > npm config set electron_mirror https://npm.taobao.org/mirrors/electron/

4. 根目录创建main.js和index.html

   ``` js
   // main.js
   const { app, BrowserWindow } = require('electron');
   
   function createWindow() {
     const win = new BrowserWindow({ widht: 800, height: 600 });
     win.loadFile('index.html');
   };
   
   app.on('ready', createWindow);
   ```

   ``` html
   <!DOCTYPE html>
   <html>
   <head>
     <meta charset="utf-8" />
     <meta http-equiv="X-UA-Compatible" content="IE=edge">
     <title>Page Title</title>
     <meta name="viewport" content="width=device-width, initial-scale=1">
   </head>
   <body>
     <h1>welcome electron</h1>
   </body>
   </html>
   ```

5. 运行`npm run start` ，查看效果

## 打包

electron目前有两种打包工具electron-builder和electron-packager

### electro-packager

1. 安装

   ```shell
   npm install electron-packager -g
   ```

2. 配置package.json

   ```json
   "scripts": {
       "pack": "electron-packager . BZ --win --arch=x64"
     },
   ```

3. 执行命令，打包后找到`.exe` 执行文件

   ``` js
   npm run pack
   ```

参考：

> 解决安装失败：https://blog.csdn.net/mocoe/article/details/86751925
>
> Electron官网：http://www.electronjs.org/