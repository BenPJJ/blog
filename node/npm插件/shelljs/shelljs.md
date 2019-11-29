# shelljs

shelljs 实现前端部署自动化

## 安装

``` shell
npm install --save-dev shelljs // 局部安装
npm install --global shelljs // 全局安装
```

## 基本配置

``` js
// shell.js
// 局部模式
const shell = require('shelljs');
// 全局模式下，不需要用shell开头
// require('shelljs/global');
const path = require('path');

if (!shell.which('node')) {
  shell.echo('Sorry, You have to execute node command!');
  shell.exit(1)
}
shell.rm('-rf', path.resolve(__dirname, './src/assets/img'));
shell.mkdir(path.resolve(__dirname, './src/assets/img'));
shell.cp('-R', path.resolve(__dirname, './src/assets/logo.png'), path.resolve(__dirname, './src/assets/img/logo.png'))
```

## Api

- **shell.which(command)**

  在环境变量path 中寻找指定命令的地址，判断该命令是否可执行，返回该命令的绝对地址

- **echo**

  在控制台输出指定内容

- **exit(code)**

  以退出码为code 退出当前进程

- **rm([options, ]file[, file...])**

  删除一个目录中一个或多个文件或目录，一旦删除，无法恢复

  - 常见参数
    - `-f` 强制删除文件
    - `-r` 递归处理目录

- **cp([options, ]source_array, dest)**

  用来将一个或多个源文件或目录复制到指定的文件或目录

  - 常见参数
    - `-R` 递归处理目录

- **cd**

  切换工作目录至指定的相对路径或绝对路径

- **ls**

  用来显示目标列表

- **mkdir([options, ]dir[, dir...])**

  创建文件夹