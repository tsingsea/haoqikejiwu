---
title: Ubuntu部署Shadowsocks-libev及simple-obfs
date: 2019-09-08 12:47:04
customizeurl: shadowsocks-libev-simple-obfs-ubuntu
categories:
- [科学上网, shadowsocks]
- [Linux, Ubuntu]
tags:
- shadowsocks
- Ubuntu
img: /images/shadowsocks.png
top: false
cover: false
coverImg: 
password: 
toc: true
mathjax: false
summary: Ubuntu部署Shadowsocks-libev及simple-obfs，纯手动搭建shadowsocks-libev服务端，安全；轻量；高速；方案成熟，全平台客户端支持。
keywords: shadowsocks,Linux,simple-obfs,加密混淆
---

## 更新源和更新软件

```
sudo apt update && sudo apt upgrade
```

Ubuntu 14.04 和 Ubuntu 16.04 用户需新增 Shadowsocks PPA 源

```
sudo apt install software-properties-common && sudo add-apt-repository ppa:max-c-lv/shadowsocks-libev && sudo apt-get update
```

## 安装 Shadowsocks-libev 和必要软件

```
sudo apt install shadowsocks-libev git vim
```

## 安装 simple-obfs

（依次运行，不需要可跳过）

```
git clone https://github.com/shadowsocks/simple-obfs.git
cd simple-obfs
git submodule update --init --recursive
./autogen.sh
./configure && make
sudo make install
```

## 配置

```
sudo nano /etc/shadowsocks-libev/config.json
```

## 填充内容到json配置文件

```
{
  "server":"0.0.0.0", // 改成 0.0.0.0 监听所有地址
  "server_port":8443, // 自定义端口
  "local_port":1080,
  "password":"FuckGFW", // 自定义密码
  "timeout":60, // 私用可改成 600
  "method":"chacha20-ietf-poly1305", // 仅推荐 AEAD 算法
  "mode":"tcp_and_udp",
  "plugin":"obfs-server", // 此行及下一行为 obfs 配置如不需要连带上一行末尾逗号一并删除
  "plugin_opts":"obfs=tls;obfs-host=yunjiasu-cdn.net"
}
```

推荐使用 AEAD 算法：

- chacha20-ietf-poly1305
- aes-256-gcm

## 管理

```
# 开启服务
sudo systemctl start shadowsocks-libev
# 停止服务
sudo systemctl stop shadowsocks-libev
# 重启服务
sudo systemctl restart shadowsocks-libev
# 开机启动
sudo systemctl enable shadowsocks-libev
```

