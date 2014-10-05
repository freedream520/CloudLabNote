sh和scp权限问题

----

ssh和scp是服务器集群管理时两个重要的命令,但是有的时候以root进行操作时会出现Permission denied错误. 这主要是由于ssh服务因为安全的考虑,默认不允许机器之间的以root身份登陆. 所以需要改一下ssh的配置文件. 具体如下:

```bash
vim /etc/ssh/sshd_config
```

将PermitRootLogin no 改为 PermitRootLogin yes

然后重启ssh服务

```bash
service ssh restart
```

ok
