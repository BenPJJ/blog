# HTTP

## DNS域名解析



## 浏览器访问网址过程

1. 对网址进行`DNS`  域名解析，得到对应的`IP` 地址；
2. 根据`IP` 地址，找到对应的服务器，发起`TCP` 的三次握手；
3. 建立`TCP` 连接后发起`HTTP` 请求；
4. 服务器响应`HTTP` 请求，浏览器得到`html` 代码；
5. 浏览器解析`html` 代码，并请求`html` 代码中的资源（如js、css、图片等）
6. 浏览器对页面进行渲染；
7. 服务器关闭`TCP` 连接；

## TCP/IP协议族

> TCP/IP 不是一个协议，而是一个协议族的统称。里面包括了IP 协议、IMCP协议、TCP协议

### - TCP/IP分层

​	TCP/IP协议族分为4层：

1. 应用层：主要是与应用通信使用到的协议，如：FTP、DNS、HTTP

2. 传输层：为应用层提供在两台机器之间数据传输，如：TCP、UDP

3. 网络层：两台机器之间传输的过程中会经过多个路由器有多条路线，网络层主要是从中选择一条路线

4. 数据链路层：用于处理连接网络的硬件部分，比如：网卡、设备驱动

### - TCP/IP分层，数据包的封装以及解包过程

在这个分层中，每次网络请求都会按照分层的顺序与对方进行通信，发送端从应用层往下走，接收端从数据链路层往上走；

举例HTTP：

1. 客户端在应用层（Http协议）发起一个HTTP请求；

2. 在传输层（Tcp协议）把从应用层收到的Http请求数据包分隔成小的数据包，并打好序；

3. 网络层（IP协议）收到数据包后选择发送路径；

4. 服务器收到数据后按照顺序往上发送，直到应用层收到数据；

   ![tcp-ip分层通信过程](img\tcp-ip分层通信过程.png)

   在发送方每经过一层，就会被加上该层的首部信息，当接收方接受到数据后，在每经过一个层会去掉对应的首部信息；

### - TCP三次握手

> TCP如何保证数据可靠到达目的地？

TCP 协议采用三次握手策略：

1. 客户端发送SYN包到服务端
2. 服务端收到客户端SYN包回复SYN+ACK
3. 客户端回复服务端ACK包

### - 为什么要三次握手

> 为什么是三次握手，而不是两次或者四次

两次握手，如果客户端自己处理异常或者服务器返回的ack信息丢失，那么客户端会认为连接失败，再次重新发送请求建立连接，但是服务端却无感知，以为连接以及正常建立，导致服务器建立无用的连接，浪费资源。

四次握手，如果三次已经足够，那就不需要四次。如果四次的话，最后ack 包丢失，那么又会出现两次握手的问题。

### - 四次挥手

1. 客户端向服务器发送FIN 希望断开连接请求；
2. 服务器向客户端发送ACK，表示同意释放连接；
3. 服务器向客户端发送一个FIN 表示希望断开连接；
4. 客户端向服务器返回一个ACK 表示同意释放连接；

### - 为什么要四次挥手

> 为什么断开连接需要四次而不是三次

服务器接收到客户端断开连接的请求后，服务器不能立即断开连接，因为有可能服务器端还有数据未发送完成，所以只能回复一个ACK 表示我已收到信息；等服务器端数据发送完成之后，再发送一个FIN 希望断开连接信息，客户端回复ACK 之后，就可以安全断开了

## HTTP

### - 为什么HTTP协议是无状态协议，怎么解决HTTP协议无状态

HTTP 协议是不保存状态的，自身不对请求和响应直接的通信状态进行保存，所以是无状态协议。

在有些场景下，需要保存用户的登录信息，所以引入了cookie 来管理状态。客户端第一次请求服务器的时候，服务器会生成cookie添加在响应头里面，以后客户端的每次请求都会带上这个cookie信息。

### - Http协议有哪些请求方式

1. GET：获取资源，所以查询操作一般用
2. POST：传输实体主体，创建更新操作用
3. HEAD：获取报文首部，如：要查询某个请求的头信息
4. PUT：传输文件
5. DELETE：删除资源，删除操作用
6. OPTIONS：查询服务器支持哪些方法
7. TRACE：追踪路径，在请求头中在Max-Forwards 字段设置数字，每经过一个服务器该数字就减一，当到0的时候就直接返回，一般通过该方法检查请求发送出去是否被篡改

### - HTTP协议状态码

HTTP 的状态码主要分为四类：

1. 2xx：成功状态码，表示请求正常处理完毕
2. 3xx：重定向状态码，表示需要附加操作才能完成请求
3. 4xx：客户端错误状态码
4. 5xx：服务端错误状态码

| 常见状态码 |                                                |
| ---------- | ---------------------------------------------- |
| 2xx        |                                                |
| 200        | 请求正常处理完成                               |
| 204        | 请求处理成功，但是没有资源返回                 |
| 206        | 表示客户端进行了范围请求                       |
|            |                                                |
| 3xx        |                                                |
| 301        | 永久性重定向，请求的资源以及被分配到了新的地址 |
| 302        | 临时重定向，希望用户并且请求新地址             |
|            |                                                |
| 4xx        |                                                |
| 400        | 客户端请求报文出现错误，通常是参数错误         |
| 401        | 客户端未认证错误                               |
| 403        | 没有权限访问该资源                             |
| 404        | 未找到请求的资源                               |
| 405        | 不支持该请求方法                               |
|            |                                                |
| 5xx        |                                                |
| 500        | 服务器异常                                     |
| 503        | 服务器不能提供服务                             |

