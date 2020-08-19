---
title: CentOS系统纯原生搭建Python版shadowsocks实现科学上网
date: 2019-07-31 18:36:08
customizeurl: shadowsocks-python-centos
categories:
- [科学上网, shadowsocks]
- [Linux, CentOS]
tags:
- shadowsocks
- CentOS
img: /images/shadowsocks.png
top: false
cover: false
coverImg: 
password: 
toc: true
mathjax: false
summary: CentOS7+系统纯原生搭建Python版shadowsocks实现科学上网，纯手动搭建shadowsocks-python服务端，安全；轻量；高速；方案成熟，全平台客户端支持。
keywords: shadowsocks,CentOS,一键脚本,秋水SSR,Python
---

### Shadowsocks纯原生搭建，整理不易，还望珍惜。

#### 安装环境：CentOS7+

#### 详细步骤

#### 1.更新&升级系统

```
yum update
yum upgrade
```

#### 2.[官网参考代码](https://pip.pypa.io/en/stable/installing/)安装pip[pip 是 Python 包管理工具，该工具提供了对Python包的查找、下载、安装、卸载的功能。]

```
pip --version  //检验是否安装pip及版本
```

```
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py  //下载官网安装脚本
	
sudo python get-pip.py  //优先运行安装python2
	
sudo python3 get-pip.py  //运行安装脚本。
```

或者直接用包管理器安装 pip，如 Debian 和 Ubuntu：

```
sudo apt-get install python-pip
```

#### 3.清除缓存

```
apt-get clean all
```

#### 4.升级pip到最新版本

```
pip install --upgrade pip
```

&

```
pip install -U pip  //upgrading pip
```

#### 5.pip 安装 python 版本的 shadowsocks

```
pip install shadowsocks
```

#### 6.安装完成后，编辑shadowsocks的配置文件，路径为/etc/shadowsocks.json，编辑命令

```
vi /etc/shadowsocks.json
```

#### 7.将以下内容根据实际情况填入json配置文件

此处进入**vim**文件编辑

```
{
	"server": "0.0.0.0",  //这里不用改，全0代表地服务器监所有可用网络。
    "server_port": 443,  //服务器端口号，1025到65535任选一。
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password": "password",  //设置登录密码。
    "method": "chacha20"  //加密方式。
    "timeout": 300,
    "mode": "tcp_and_udp",
    "fast_open": false
}
```

进阶配置多端口：

```
{
	"server":"0.0.0.0",
	"local_address": "127.0.0.1",
	"local_port":1080,
	"port_password":{
	"8381": "D77b73E578",
	"8382": "53AFf96aEf",
	"8383": "6E18a11eA2",
	"8384": "OTU0OWQ2Nz"
	},
	"timeout":300,
	"method":"aes-256-cfb",
	"fast_open": false
}
```

#### 8.编辑自启动脚本，编辑命令

```
vi /etc/systemd/system/shadowsocks.service
```

#### 9.将以下内容根据实际情况填入server配置文件

这里进入vim文件编辑，脚本内容如下：

```
[Unit]
Description=Shadowsocks
[Service]
TimeoutStartSec=0
ExecStart=/usr/bin/ssserver -c/etc/shadowsocks.json
[Install]
WantedBy=multi-user.target
```

#### 10.启动 shadowsocks 服务

```
systemctl enable shadowsocks
systemctl start shadowsocks
systemctl stop shadowsocks
systemctl status shadowsocks
```

#### 11.查看状态

```
systemctl status shadowsocks -l
```

*如果显示active(running)就表示服务器配置成功。没有成功的话可以返回“安装配置shadowsocks”认真按介绍再来一次。*

#### 12.自愿安装bbr

#### 13.各种下载地址

[Win客户端](https://github.com/shadowsocks/shadowsocks-windows/releases/download/4.1.10.0/Shadowsocks-4.1.10.0.zip)

[Mac客户端](https://github.com/shadowsocks/ShadowsocksX-NG/releases/download/v1.9.4/ShadowsocksX-NG.1.9.4.zip)

[安卓客户端](https://github.com/shadowsocks/shadowsocks-android/releases/download/v5.0.6/shadowsocks--universal-5.0.6.apk)

[Linux客户端](https://github.com/shadowsocks/shadowsocks-qt5/releases/download/v3.0.1/Shadowsocks-Qt5-3.0.1-x86_64.AppImage)