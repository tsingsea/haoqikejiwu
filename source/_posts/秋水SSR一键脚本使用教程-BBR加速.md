---
title: 秋水SSR一键脚本使用教程+BBR加速
date: 2019-08-09 12:33:55
customizeurl: shadowsocksr-qiushui-sh
categories:
- [科学上网, shadowsocksr]
tags:
- shadowsocksr
img: /images/shadowsocksr.png
top: false
cover: false
coverImg: 
password: 
toc: true
mathjax: false
summary: 使用秋水大神的一键脚本进行ssr的安装
keywords: shadowsocksr,一键脚本,秋水SSR,BBR
---

## 获得root权限

```
sudo -i
```

## 秋水大神的一键脚本进行ssr的安装

```
wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
chmod +x shadowsocks-all.sh
./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
```

1. 执行以上脚本
2. 选择第二个选项
3. 输入任意密码
4. 输入端口号：必须`0-65535`之间
5. 选择**加密**方式：`11`
6. 选择**协议protocol**：`3`
7. 选择混淆**obfs**：`8`
8. 回车键开始安装
9. 当屏幕上打印出**节点信息**后，表示安装完成。注意：请记下配置信息，以便客户端配置时使用。

## 一键安装bbr

```
wget "https://github.com/chiakge/Linux-NetSpeed/raw/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

bbr版本自由选择，一般选择：`BBRplus`，安装完成后，恭喜你，搭建完成。