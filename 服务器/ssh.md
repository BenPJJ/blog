# ssh

## centos 7 操作SSH/SSHD服务

1）查看状态

``` shell
# systemctl status sshd.service
```

2）启动服务

``` shell
# systemctl start sshd.service
```

3）重启服务

```shell
# systemctl restart sshd.service
```

4）开机自启

``` shell
# systemctl enable sshd.service
```

