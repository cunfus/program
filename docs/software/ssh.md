# ssh

!!! abstract
    关于 ssh 配置的常见方式。


终端下最常见的操作就是远程到服务器，一次次输入密码既不安全，又让人比较头疼。

使用 ssh-keygen 生成私钥和公钥，登记私钥到本地的 ssh 配置文件里，发送公钥到远程服务器（需要输入一次密码），这样后面再连接远程服务器时，就做到了免密登陆。

操作步骤如下：

```shell
# 1. 生成私钥和公钥
$ ssh-keygen -t rsa -f ecs

# 2. 私钥登记到本地 ssh 配置文件
$ vim ~/.ssh/config

Host ecs
    HostName xx.xx.xx.xx
    User user-name
        IdentityFile ~/.ssh/server/ecs

Host ecs2
    HostName xx.xx.xx.xx
    User user-name
        IdentityFile ~/.ssh/server/ecs2

# 3. 发送公钥到远程服务器
$ ssh-copy-id -i ecs.pub  user-name@xx.xx.xx.xx

# 4. 免密连接
$ ssh ecs

# 5. 远程执行命令
$ ssh ecs 'bash git.sh test'
```
