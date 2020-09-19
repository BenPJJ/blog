# nginx

## 基本配置

``` json
user	nobody;	#设置nginx服务的系统使用用户
worker_processes	1;	#工作进程数 一般情况与CPU核数保持一致
error_log		logs/error.log;	#nginx的错误日志
pid        logs/nginx.pid;	#nginx启动时的pid
events {
    worker_connections  1024; #每个进程允许最大连接数
}
```

在配置文件`nginx.conf` 中的http区域内，配置无数个server，每个server对应这一个虚拟主机或者域名

``` json
http {
  ... ... 
  server {
  	listen 80 #监听端口
  	server_name localhost #地址
  	
  	location / {	#访问首页路径
  		root /xxx/xxx/index.html #默认目录
  		index index.html index.htm #默认文件
		}
		error_page 500 504 / 50x.html #当出现以上状态码时重新定义到50x.html
		location = /50x.html { #当访问50x.html时
			root /xxx/xxx/html #50x.html 页面所在位置
		}
	}
	server {
    ... ...
  }
}
```

一个`server` 可以出现多个location，对不同的访问路径进行不同情况的配置

### 3. `http` 的配置

``` json
http {
  sendfile on; #高效传输文件的模式 一定要开启
  keepalive_timeout 65; #客户端服务器请求超时时间
  log_format main xxx; #定义日志格式 代号为main
  access_log logs/access.log main; #日志保存地址 格式代码 main
}
```



