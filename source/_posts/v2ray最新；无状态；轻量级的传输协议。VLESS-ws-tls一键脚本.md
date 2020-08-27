---
title: v2ray最新、无状态、轻量级的传输协议。VLESS+ws+tls一键脚本
date: 2020-08-25 19:02:49
customizeurl: v2fly-vless+ws+tls
categories:
- [科学上网, v2ray]
- [科学上网, v2fly]
- [一键脚本]
tags:
- v2ray
- v2fly
- 一键脚本
description: 继v2ray官方脚本转型v2fly，VLESS+ws+tls一键安装脚本！VLESS协议！v2ray最新、无状态、轻量级的传输协议。v2Ray客户端和服务器之间的桥梁协议。
---

## 前言

1. VMESS是v2ray的传输协议。但是在5月v2ray爆出危险新闻之后，随之v2ray官方业务转型v2fly，诞生VLESS协议。
2. VLESS是一个无状态的轻量传输协议，它分为入站和出站两部分，可以作为 v2ray客户端和服务器之间的桥梁。VLESS 不依赖于系统时间，认证方式同样为 UUID，但不需要 alterID。
3. 今天为大家带来的是一键安装VLESS+ws+tls的脚本，很简单。

## 准备工作

1. VPS一台，重置主流版本的操作系统
2. 域名一个，做好解析，同v2ray一个道理

## 开始搭建

1. 此脚本需要GIT环境用于拉取伪装网站源文件，不懂GIT的执行

   ```
   yum install -y git  #CentOS安装命令
   apt install -y git  #Debian/Ubuntu安装命令
   ```

   懂的你怎么开心怎么来

2. 一键脚本如下：

   ```
   wget -N --no-check-certificate -q -O install.sh "https://raw.githubusercontent.com/wulabing/V2Ray_ws-tls_bash_onekey/master/install.sh" && chmod +x install.sh && bash install.sh
   ```

3. 访问你绑定的域名即可看到网站！！！

## VLESS支持的客户端

（截止到2020年8月15日）

### 图形客户端

#### [v2RayNG](https://github.com/2dust/v2rayNG)

- V2RayNG 是一个基于 V2Ray 内核的 Android 应用，它可以创建基于 VMess 的 VPN 连接。

#### [v2rayN](https://github.com/2dust/v2rayN)

- V2RayN 是一个基于 V2Ray 内核的 Windows 客户端。

#### [v2rayU](https://github.com/yanue/V2rayU)

- V2rayU，基于 V2Ray 核心的 macOS 客户端，使用 Swift 4.2 编写，支持 VMess、Shadowsocks、SOCKS5 等服务协议，支持订阅，支持二维码、剪贴板导入、手动配置、二维码分享等。

#### [Qv2ray](https://github.com/Qv2ray/Qv2ray) 

- 跨平台 V2Ray 客户端，支持 Linux、Windows、macOS，可通过插件系统支持 SSR / Trojan / Trojan-Go / NaiveProxy 等协议，不支持批量测速，不支持自动更新，不建议小白使用

### 支持VLESS软路由插件

（截止到2020年8月15日）

#### [PassWall](https://github.com/xiaorouji/openwrt-package)

- PassWall（v3.9.35+），支持 OpenWRT
