# Linux安装

##	Linux镜像下载地址

```html
http://mirrors.aliyun.com/centos/7/isos/x86_64/
```

## Minimal

此版本无网络,需要先安装网络

```shell
cd /etc/sysconfig/network-scripts/
```

注意文件`ifcfg-ensxxx` 笔者这里是33 即`ifcfg-ens33` 

```shell
vi ifcfg-ens33
```

修改并增加配置

```shell
BOOTPROTO=static
ONBOOT=yes
IPADDR=192.168.47.201
NETMASK=255.255.255.0
GATEWAY=192.168.47.2
DNS1=114.114.114.114
```

安装ifconfig命令

```shell
sudo yum install net-tools
```



