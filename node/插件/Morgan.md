# Morgan

日志记录中间件，能对用户的行为和请求时间进行记录

## 安装

``` js
npm install --save-dev morgan
```

## 使用

``` js
const express = require('express');
const logger = require('morgan');

const app = express();
app.use(logger('short'));
```