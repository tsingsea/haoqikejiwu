---
title: 使用snap工具手动搭建shadowsocks-libev
date: 2019/7/13 20:46:25
customizeurl: shadowsocks-libev-snap
categories:
- [科学上网, shadowsocks]
- [Linux]
tags:
- shadowsocks
- Linux
img: /images/shadowsocks.png
top: true
cover: true
coverImg: 
password: 
toc: true
mathjax: false
summary: 使用snap工具手动搭建shadowsocks-libev服务端，安全；轻量；高速；方案成熟，全平台客户端支持。
keywords: shadowsocks,Linux,snap工具
---
## 前言

适用于Debian9+系统，官方推荐快速安装方式，简单高效，不用担心后门脚本捣乱，纯手动搭建。

## 更新系统

```
sudo apt update
```

## 安装snap工具

```
sudo apt install snapd
sudo snap install core
```

## 使用snap工具安装ss-libev

```
sudo snap install shadowsocks-libev
```

## 进入snap/bin目录

```
cd /snap/bin
```

## 编辑json配置文件

```
nano config.json
```

## 填充如下内容

```
{
    "server":"0.0.0.0",
    "nameserver": "8.8.8.8",
    "server_port":443,
    "local_port":1080,
    "password":"password",
    "timeout":600,
    "no_delay":true,
    "fast_open":true,
    "reuse_port":true,
    "method":"chacha20-ietf-poly1305"
}
```

## 以守护程序运行

ps：以守护程序运行，执行一次开启命令，只要不重启服务器，一直保持运行，重启服务器需要再次执行以下命令。

```
/snap/bin/shadowsocks-libev.ss-server -c /snap/bin/config.json -f /snap/bin/ss-server-pid
```