# Centos

## 概念

### 1. linux下软件安装

1）yum安装

​	yum形式类似于npm安装，简单快捷，自动安装相关依赖。

2）源码安装

​	源码安装需要下载源码然后本机编译，可以实现个性化定制。

3）rpm安装

​	安装与yum类似，只不过安装的模块来源不是yum官方镜像，而是本地资源。

### 2. 目录意义

1）/ect

​	`/ect` 是linux下专门用来放配置文件的一个目录

2）/usr

​	`/usr` 可以理解为window下的`C:\Progran Files`

## 常用命令

1）文件与目录操作

``` json
# cd
cd /home //进入‘/home’目录
cd .. //返回上一级目录
cd ../.. //返回上两级目录

# cp
cp file1 file2 //将file1复制为file2
cp -a dir1 dir2 //复制一个目录
cp -a /tmp/dir1 . //复制一个目录到当前工作目录（.代表当前目录）

# ls
ls //查看目录中的文件
ls -a //显示隐藏文件
ls -l //显示详细信息
ls -lrt //按时间显示文件（l表示详细列表、r表示反向排序、t表示按时间排序）

# pwd
pdw //显示工作目录

# mkdir
mkdir dir1 //创建‘dir1’目录
mkdir dir1 dir2 //同时创建两个目录
mkdir -p /tmp/dir1/dir2 //创建一个目录树

# mv
mv dir1 dir2 //移动/重命名一个目录

# rm
rm -f file1 //删除‘file1’
rm -rf dir1 //删除‘dir1’目录及其子目录内容

# rpm
```

2）权限操作

​	文件或目录权限的控制分别以：读取、写入、执行3种。

``` json
# chmod 更改文件或目录的权限
如：
chmod 600 .ssh/authorized_keys
```

```json
# chown 更改目录所有者和所属组
chown [参数] [所有者：所属组] [文件|目录]
-R //递归处理，将指令目录下的所有文件及子目录一并处理

如：
chown -R git:git git
```

3）其他

``` shell
# netstat -lnp|grep 80 //检查端口被哪个进程占用
```

