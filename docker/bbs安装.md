# bbs安装

## 1.安装镜像

```shell
# 拉镜像
$ docker pull docker3865146/bozhong_ubuntu_php74_nginx:latest

# 运行容器
$ docker run --name ubuntu_sytem -p 80:80 -v D:\code.bzdev.net:home\www -it -d docker3865146/bozhong_ubuntu_php74_nginx /bin/bash -c "/etc/rc.local; /bin/bash"

# 查看镜像
$ docker ps

# 进入镜像
$ docker exec -it ubuntu_sytem /bin/bash
	# 启动nginx
root@7c3afcf0ed9f:/# /etc/init.d/nginx start
	# 启动php
root@7c3afcf0ed9f:/# /etc/init.d/php7-fpm start
	# 如果需要修改php端口
root@7c3afcf0ed9f:/# cd /usr/local/php/etc/
root@7c3afcf0ed9f:/usr/local/php/etc# vim php-fpm.d/www.conf
root@7c3afcf0ed9f:/usr/local/php/etc# /etc/init.d/php7-fpm start
	# 进入nginx配置
root@7c3afcf0ed9f:/usr/local/php/etc# cd /etc/nginx/sites-enabled

	# 进入映射目录
root@7c3afcf0ed9f:/usr/local/php/etc# cd /home/www
	# 查看文件夹（ls 和 ll区别）
	# ls，仅罗列出当前文件名和目录名
	# ll，罗列出当前文件或目录的详细信息
root@7c3afcf0ed9f:/home/www# ll
```

## 2. 配置nginx

```shell
$ docker ps
$ docker exec -it ubuntu_sytem /bin/bash
root@7c3afcf0ed9f:/# cd /etc/nginx/sites-enabled/
root@7c3afcf0ed9f:/etc/nginx/sites-enabled# l
default@
root@7c3afcf0ed9f:/etc/nginx/sites-enabled# rm default
root@7c3afcf0ed9f:/etc/nginx/sites-enabled# vim bbs.seedit.com
root@7c3afcf0ed9f:/etc/nginx/sites-enabled# mkdir /home/logs
root@7c3afcf0ed9f:/etc/nginx/sites-enabled# /etc/init.d/nginx reload
* Reloading nginx configuration nginx
# 查看日志
root@7c3afcf0ed9f:/etc/nginx/sites-enabled# tail -f /var/log/nginx/error.log


```

## 3. 配置本地host

``` shell
# hosts地址：C:\Windows\System32\drivers\etc\hosts
# 找文件小技巧，字母定位，敲响文件的第一个字母，就可以定位对应文件开头

# pc
$ 127.0.0.1  	bbs.pjj.bzdev.net
# m
$ 127.0.0.1  	m.pjj.bzdev.net
```

## 4. 异常

``` shell
# 开启本地服务，使用一会有时会出现空白页面，清除缓存就可以

1）在bbs.seedit.com/htdoc/data/template路径下，清除掉缓存
或
2）在容器命令行中，输入cd /home/www/bbs.seedit.com/htdoc/data/template，然后rm *
```

## 5. 正常使用

``` shell
## 退出软件再启动步骤
# 启动docker desktop
# 查看所有的容器
$ docker ps -a
# 启动容器
$ docker start ubuntu_sytem
# 进入容器
$ docker exec -it ubuntu_sytem /bin/bash
# 开启nginx
root@7c3afcf0ed9f:/# /etc/init.d/nginx start
# 关闭nginx
root@7c3afcf0ed9f:/# /etc/init.d/nginx stop
# 退出容器
root@7c3afcf0ed9f:/# exit

## 平常不关闭软件步骤
# 查看运行的容器
$ docker ps
# 进入容器
$ docker exec -it ubuntu_sytem /bin/bash
# 开启nginx
root@7c3afcf0ed9f:/# /etc/init.d/nginx start
# 关闭nginx
root@7c3afcf0ed9f:/# /etc/init.d/nginx stop
# 退出容器
root@7c3afcf0ed9f:/# exit
```

参考文献：

> 播种wiki： http://wiki.bozhong.com/bbs/start
>
> 裕冲合成镜像：http://blog.liaoyuchong.com/index/article?id=73