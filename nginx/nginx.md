# nginx

## 安裝

> 1. 官网下载需要的版本（
>
>    ​	Mainline version：最新版本
>
>    ​	Stable version：稳定版本
>
>    ​	Legacy versions：历史版本
>
>    ）
>
> 2. 解压nginx（
>
>    ​	conf：配置文件目录
>
>    ​	html：默认站点目录
>
>    ​	logs：日志目录
>
>    ）

## 命令行使用

在`nginx.exe` 目录

### 1. 启动

> start nginx

### 2. 关闭

> nginx -s stop  // 快速停止nginx
>
> nginx -s quit  // 完整有序的停止nginx

### 3. 检查nginx是否启动

> 1. 直接在浏览器地址输入http:// localhost:80，出现页面说明启动成功
> 2. tacklist /fi "imagename eq nginx.exe"，出现结果说明启动成功

### . 其他

> nginx -s reload  // 修改配置后重新加载生效
>
> nginx -s reopen  // 重新打开日志文件