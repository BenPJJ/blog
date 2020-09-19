# git生成SSH Key

## 1. 进入.ssh文件夹

> cd ~/.ssh/

## 2. 配置全局得name和email

> git config --global user.name "用户名"
>
> git config --global user.email "个人邮箱"

## 3. 生成key

> ssh-keygen -t rsa -C "个人邮箱"

``` ssh
// 连续按三次回车，这里设置的密码就为空了，并且创建了key

$ ssh-keygen -t rsa -C "2535103724@qq.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/jj/.ssh/id_rsa):
/c/Users/jj/.ssh/id_rsa already exists.
Overwrite (y/n)? y
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/jj/.ssh/id_rsa.
Your public key has been saved in /c/Users/jj/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:4cVmdWfFXmu0KSbgkpoqeb/8APVbNG6EUznvUWKbuPA 2535103724@qq.com
The key's randomart image is:
+---[RSA 2048]----+
|         .. . ..=|
|        o= + o +o|
|     . o++@ = ..=|
|    . .==B.* o =.|
|   .  o.S+o + o  |
|    .o  +E .     |
|  . .. .         |
| o o. .          |
|  o .+o.         |
+----[SHA256]-----+

// 最后得到了两个文件：id_rsa 和 id_rsa.pub
```

## 4. 复制公秘钥id_rsa.pub到github

## 5. 测试是否添加成功

> ssh -T git@github.com

提示：`Hi BenPJJ! You've successfully authenticated, but GitHub does not provide shell access.`  说明添加成功

## 6. 如果连接不成功

> ssh: connect to host github.com port 22: Connection timed out
>
> fatal: Could not read from remote repository.
>
> Please make sure you have the correct access rights
>
> and the repository exists.

找到git安装路径下的Git\etc\ssh\ssh_config文件，打开在后面添加上下面这段代码，再次连接就成功啦

```
Host github.com

User git

Hostname ssh.github.com

PreferredAuthentications publickey

IdentityFile ~/.ssh/id_rsa

Port 443
```

