# Docker

## docker-nginx使用

1. 查看docker容器

   > docker images

2. 安装nginx

   - 在 [docker hub](https://hub.docker.com/) 搜索nginx，查看安装命令

     > docker pull nginx:latest

   ![nginx](D:\blog\docker\img\nginx-install.png)

3. 启动nginx

   > docker run --name ngx_demo -p 8080:80 -d nginx

   - --name 表示给这个container取个名字
   - -p 8080:80 表示将docker container的80端口映射到主机的8080端口
   - -d 表示让container运行在后台，不然这个会占据你的命令行窗口

4. 查看nginx container启动情况**（桌面版点击`dashboard`）**

   > docker ps

5. 在浏览器中访问

   > http://localhost:8080

   ![nginx](D:\blog\docker\img\nginx-start.png)

6. 查看container log

7. 关闭nginx

   > docker stop 6dc8a63773df
   >
   > docker stop ngx_demo

   - stop方式

     - 通过CONTAINER ID（通过docker ps查看）
     - 通过NAMES（通过docker ps查看）
     - 通过dashboard（桌面）


8. 挂载本地目录到镜像中

   - 在容器中相关位置分别是：

     > 日志：/var/log/nginx
     >
     > 配置文件：/etc/nginx
     >
     > 项目：/usr/share/nginx/html

   - 配置

     > docker run --name nginx_test -d -p 8080:80 -v D:/nginx/conf/nginx.conf:/etc/nginx/nginx.conf -v D:/nginx/html:/usr/share/nginx/html -v D:/nginx/logs:/var/log/nginx -v D:/nginx/conf.d:/etc/nginx/conf.d nginx

9. 修改nginx配置后，需要进入容器中重启下nginx

   > docker exec -it nginx_test /bin/bash
   >
   > nginx -s reload