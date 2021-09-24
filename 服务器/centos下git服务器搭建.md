# centos下git服务器搭建

安装git

``` shell
# git --version //查看git是否安装
# yum install -y git //安装
# git --version //查看是否安装成功
```

创建一个git用户组和用户，用来运行git服务

```shell
# groupadd git
# useradd git -g git
# passwd git
```

创建证书登录

```shell
# cd /home/git
# mkdir .ssh
# chmod 700 .ssh
# touch .ssh/authorized_keys
# chmod 600 .ssh/authorized_keys
#	cd /home
# chown -R git:git git
```

4）服务端创建RSA

``` json
# 进入 /etc/ssh 目录，编辑 sshd_config，打开以下三个配置的注释：
RSAAuthentication yes # 可能不存在该选项
PubkeyAuthentication yes
AuthorizedKeysFile      .ssh/authorized_keys

# 保存并重启 sshd 服务：
systemctl restart sshd.service
```

5）在客户端将本地公钥导入服务器`/home/git/.ssh/authorized_keys` 文件

```shell
ssh git@47.107.83.157 'cat >>.ssh/authorized_keys' < ~/.ssh/id_rsa.pub
git@47.107.83.157's password: xxx # 密码是git的密码
```

6）centos服务端初始化git仓库

```json
# cd /home
# mkdir demo
# chown -R git:git codebase
# git init --bar robot.git
# chown -R git:git robot.git
```

7）客户端操作

``` json
# 1初始化本地产库
$ git init
# 2添加关联远程仓库
$ git remote add origin ssh://git@47.107.83.157:/home/codebase/robot.git
# 3拉取分支（新建仓库需要上传文件后才能查看否则会报错）
$ git fetch origin master
# 补坑第三步
$ git add .
$ git commit -m "新建仓库"
$ git push --set-upstream origin master
# 4创建分支
$ git checkout -b dev
# 5推送至远程分支
$ git push origin dev:dev
# 6查看分支
$ git branch
# 7查看远程分支
$ git branch -r
# 8修改分支内容后，查看分支状态
$ git status
# 添加修改文件
$ git add -A
# 提交
$ git commit -m "备注"
# 推送至远程分支
$ git push origin dev
# 合并至远程分支
$ git checkout origin
$ git merge dev
$ git push -u origin master
# 更新分支
$ git pull origin master
# 删除远程分支
$ git push origin --delete dev
```

8）git服务器管理代码

``` json
# git log //查看提交记录
# git show //查看某次提交的详情
# git diff //比较文件变动
```

注意：

为什么私有的git服务器上无法查看上传的代码？

​	因为是创建git仓库的命令`git init --bar xxx.git` 是用于创建一个裸仓库，没有工作区。

​	服务器上的git仓库只保存git历史提交的版本信息，纯粹是为了共享，所以不让用户直接登录到服务器上去改工作。