# MongoDB

## 1. 安装

## 2. 配置本地windows mongodb服务

配置本地windows mongodb服务，开机自启动，可直接手动启动关闭，可通过命令行net start MongoDB启动

#### 步骤：

1. 在data文件下创建一个log文件夹（用于存放日志文件）

2. 在mongodb下新建配置文件mongo.config

   写入：

   ``` 
   dbpath="D:Software\MongoDB\data\db"
   logpath="D:Software\MongoDB\data\log\mongo.log"
   ```

3. 用管理员身份打开cmd

4. cmd找到"D:\Software\MongoDB\bin"目录下，输入：

   ```
   mongod --config "D\Software\MongoDB\mongo.config" --install --serviceName "MongoDB"
   ```

   接着输入：

   ```
   # 启动服务
   net start MongoDB
   
   # 停止服务
   net stop MongoDB
   ```

   查看本地的服务：

   ```
   "w + r"：services.msc
   ```