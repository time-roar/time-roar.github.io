# Linux常见问题

##	linux资源不可用,资源暂时不可用
```shell
su -m -c 'ulimit -a' username
```

提示如下

```shell
su: 无法设置用户ID: 资源暂时不可用
```

按经验看就是username用户开了太多线程，达到系统最大限制(默认1024)

```shell
ps –eL | wc -l
```

显示如下

```shell
2219
```

总线程数超过1024，有可能是线程满的问题。不过这台服务器已经调整过用户线程限制了，为何还会出现这个问题呢？

查看用户环境变量：

```shell
cat /etc/profile.d/ulimit.sh
```

打印如下

```properties
#!/bin/bash
[ "$(id -u)" == "0" ] && ulimit -n 1048576
ulimit -u 10000
```

系统限制配置，/etc/security/limits.conf：

* soft nproc 10000

* hard nproc 10000

* soft nofile 1048576

* hard nofile 1048576

验证一下，结果还是设置无效：

```shell
su -m -c 'ulimit -u' nobody
```

结果还是

```shell
 1024
```

最后确定是由于CentOS 6.4版本新增了限制配置 ，以保证root用户无限制。此配置会覆盖主配置文件的设定：

查看文件如下:

```shell
cat /etc/security/limits.d/90-nproc.conf 
```

显示文件如下

```proper
Default limit for number of user's processes to prevent
accidental fork bombs.
See rhbz #432903 for reasoning.

soft    nproc     1024
root    nproc     unlimited
```

OK，问题就此定位！

解决办法：删除 /etc/security/limits.d/90-nproc.conf 文件中1024那一行。

注意：不推荐删除此文件，一方面root无限制的配置丢了；另一方面如果此配置文件不存在，执行系统升级时可能又被写入；文件存在时，升级系统时，即使此文件需要更新，也不会被覆盖而是生成 90-nproc.conf.rpmnew。
