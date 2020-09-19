# Docker

## Docker两个重要概念

1. 一个是容器（Container）：容器特别像一个虚拟机，容器中运行着一个完整的操作系统。可以在容器中装Nodejs，可以执行`npm install` ，可以做一切你当前操作系统能做的事情。

2. 另一个是镜像（Image）：镜像是一个文件，它是用来创建容器的。Docker镜像类似于`Win7纯净版.rar` 文件

在Docker中，通常称当前使用的真实操作系统为“宿主机”（Host）

## 安装Docker

一万个字省略。。。（后面补上）

## 运行Docker

### 1. 简单例子

搭建一个能够托管静态文件的Nginx服务器

容器运行程序，而容器哪来的？容器是镜像创建出来的。那镜像又是哪里来？

镜像是通过一个Dockerfile打包来的，它非常像前端的`package.json` 文件

``` shell
// 关系图
Dockerfile：类型于package.json
|
V
Image：类似于`Win7纯净版.rar`
|
V
Container：一个完整操作系统

```



