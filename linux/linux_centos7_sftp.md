# centos7下配置sftp且限制用户访问目录
## 1. 添加账户
$ useradd images
$ passwd images

## 2.修改/etc/ssh/sshd_config
注释掉 Subsystem sftp /usr/libexec/openssh/sftp-server
在下面添加
```
Match User images
        ForceCommand internal-sftp
        ChrootDirectory /home/images
```
## 3.修改/home/images 目录权限
$ cd /home
$ chown root:root images

## 4.重启ssh
$ systemctl restart sshd

## 5.设置可写目录
$ cd /home/images
$ mkdir write
$ chown images:images write

## 6.filezilla 连接测试

参考：
[如何将SFTP用户限制在某个目录下？](http://www.jbxue.com/LINUXjishu/22628.html)
[centos下配置sftp且限制用户访问目录](https://segmentfault.com/a/1190000000441260)


