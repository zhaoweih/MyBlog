---
title: '如何启用Shadowsocks的多端口'
date: 2019-06-01 11:30:32
tags: [shadowsocks,outline,翻墙]
categories: 翻墙
---

**原文地址(原文目前已经被删除 本文属于备份文章  )：[如何启用Shadowsocks的多端口](https://teddysun.com/532.html)**  

一键脚本默认只会开启单个端口以供使用。之所以这么做，是因为考虑到一般都是个人使用才会自己搭建属于自己的 Shadowsocks 服务端，所以在安装交互的时候，默认只要求输入某个端口即可。但如果你想要小范围内分享，那么你可能需要开启多个端口。 目前主流的四个版本实际上都是支持多端口的，只不过开启的方法不太一样，本文的重点就是写一下针对不同版本的 Shadowsocks 如何开启多端口。

注意：本文是以四合一版的正确安装和使用为前提条件的。

## Shadowsocks-Python

Shadowsocks-Python 版的配置文件路径 /etc/shadowsocks-python/config.json，下面以修改该配置文件来说明。 在 Linux 下建议使用 vim 或者 nano 来编辑此配置文件。具体如何使用这两种编辑器，这里不多说明，可自行去搜索相关用法。 Shadowsocks-Python 版多端口配置文件示例：

```javascript
{
    "server":"0.0.0.0",
    "local_address":"127.0.0.1",
    "local_port":1080,
    "port_password":{
         "9000":"password0",
         "9001":"password1",
         "9002":"password2",
         "9003":"password3",
         "9004":"password4"
    },
    "timeout":300,
    "method":"your_encryption_method",
    "fast_open": false
}
```

重点在于 port_password 字段的修改。 你想要多少端口就添加多少端口，注意需要符合 json 格式，里面的最后一行后面是没有英文逗号的，整个大括号的最后需要有一个英文逗号。 修改完成后，保存配置文件，重启之。命令如下：

```javascript
$ /etc/init.d/shadowsocks-python restart
```

## ShadowsocksR

ShadowsocksR 版的配置文件路径 /etc/shadowsocks-r/config.json，下面以修改该配置文件来说明。 ShadowsocksR 版多端口配置文件示例：

```javascript
{
    "server":"0.0.0.0",
    "server_ipv6": "[::]",
    "local_address":"127.0.0.1",
    "local_port":1080,
    "port_password":{
        "9000":"password0",
        "9001":"password1",
        "9002":"password2",
        "9003":"password3",
        "9004":"password4"
    },
    "timeout":300,
    "method":"your_encryption_method",
    "protocol": "your_protocol",
    "protocol_param": "",
    "obfs": "your_obfs",
    "obfs_param": "",
    "redirect": "",
    "dns_ipv6": false,
    "fast_open": false,
    "workers": 1
}
```

重点在于 port_password 字段的修改。 你想要多少端口就添加多少端口，注意需要符合 json 格式，里面的最后一行后面是没有英文逗号的，整个大括号的最后需要有一个英文逗号。 修改完成后，保存配置文件，重启之。命令如下：

```javascript
$ /etc/init.d/shadowsocks-r restart
```

## Shadowsocks-Go

Shadowsocks-Go 版的配置文件路径 /etc/shadowsocks-go/config.json，下面以修改该配置文件来说明。 Shadowsocks-Go 版多端口配置文件示例：

```javascript
{
    "port_password":{
         "9000":"password0",
         "9001":"password1",
         "9002":"password2",
         "9003":"password3",
         "9004":"password4"
    },
    "method":"your_encryption_method",
    "timeout":300
}
```

重点在于 port_password 字段的修改。 你想要多少端口就添加多少端口，注意需要符合 json 格式，里面的最后一行后面是没有英文逗号的，整个大括号的最后需要有一个英文逗号。 修改完成后，保存配置文件，重启之。命令如下：

```javascript
$ /etc/init.d/shadowsocks-go restart
```

## Shadowsocks-libev

Shadowsocks-libev 版是唯一不能单纯靠修改配置文件来开启多端口的。

不过，开发者单独开发了一个 ss-manager 来管理和开启多端口，其工作原理大致如下：

调用 ss-server 并根据配置文件里的多个端口号，在当前用户目录下生成隐藏文件夹 .shadowsocks 以及拆分配置文件为 .shadowsocks_端口号.conf，并以此创建新的进程，再生成 .shadowsocks_端口号.pid 来保存进程的 pid 信息。 最终，创建出来的 ss-server 进程数和配置文件里的端口数相同。也就是说，每个端口需要开启一个 ss-server 进程。

于是就简单写了一个用于 Shadowsocks-libev 版多用户管理 ss-manager 的启动脚本，可以通过编辑 json 配置文件 /etc/shadowsocks-manager/config.json 的形式，启动和停止多端口的 libev 版服务端。 下面说一下用法。

### 下载该启动脚本并赋予执行权限。

```javascript
$ wget -O /etc/init.d/shadowsocks-manager https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-manager
$ chmod 755 /etc/init.d/shadowsocks-manager
```

### 新建存放配置文件的目录

```javascript
$ mkdir /etc/shadowsocks-manager
```

### 创建多端口配置文件，/etc/shadowsocks-manager/config.json

示例：

```javascript
{
    "server":"0.0.0.0",
    "port_password":{
         "9000":"password0",
         "9001":"password1",
         "9002":"password2",
         "9003":"password3",
         "9004":"password4"
    },
    "timeout":300,
    "user":"nobody",
    "method":"your_encryption_method",
    "nameserver":"8.8.8.8",
    "mode":"tcp_and_udp"
}
```

关于配置文件，更多选项，请参考：     <https://github.com/shadowsocks/shadowsocks-libev/blob/master/doc/shadowsocks-libev.asciidoc>

### 使用启动脚本

```javascript
启动：/etc/init.d/shadowsocks-manager start
停止：/etc/init.d/shadowsocks-manager stop
重启：/etc/init.d/shadowsocks-manager restart
查看状态：/etc/init.d/shadowsocks-manager status
```

## 共通步骤

如果你是在 CentOS 系统里运行的，也许会需要将配置文件里对应的端口在防火墙里打开。 CentOS 6 一般是使用 iptables，先确认一下状态：

```javascript
$ /etc/init.d/iptables status
```

如果是处于运行中，那么打开新端口的命令如下：

```javascript
$ iptables -I INPUT -m state --state NEW -m tcp -p tcp --dport 新端口号 -j ACCEPT
$ iptables -I INPUT -m state --state NEW -m udp -p udp --dport 新端口号 -j ACCEPT
```

保存并重启 iptables，命令如下：

```javascript
$ /etc/init.d/iptables save
$ /etc/init.d/iptables restart
```

显示 iptables 一览，并确认端口是否添加成功：

```javascript
$ iptables -L -n
```

CentOS 7 一般是使用 firewalld，先确认一下状态：

```javascript
$ systemctl status firewalld
```

如果是处于运行中，那么打开新端口的命令如下：

```javascript
$ firewall-cmd --permanent --zone=public --add-port=新端口号/tcp
$ firewall-cmd --permanent --zone=public --add-port=新端口号/udp
```

重新加载 firewalld，命令如下：

```javascript
$ firewall-cmd --reload
```

显示 firewall 一览，并确认端口是否添加成功：

```javascript
$ firewall-cmd --list-all
```

Debian 或 Ubuntu 默认一般是不开启防火墙的，当然也有可能出现特殊情况已经开启了，那么同样需要将配置文件里对应的端口在防火墙里打开。 当然，如果你嫌麻烦，那么可以直接将防火墙关闭。 iptables 的关闭方法：

```javascript
$ /etc/init.d/iptables stop
```

关闭开机自启动

```javascript
$ chkconfig iptables off
```

firewalld 的关闭方法：

```javascript
$ systemctl stop firewalld
```

关闭开机自启动

```javascript
$ systemctl disable firewalld
```

另外，如果你使用的是大公司的 Cloud 产品，比如 AWS，Google Cloud，Azure，阿里云等等，也许还需要在后台的控制面板里将对应的通信端口打开。这里就不多说明了，每家的方法大同小异。