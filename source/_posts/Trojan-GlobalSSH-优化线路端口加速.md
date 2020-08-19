---
title: Trojan+GlobalSSH+优化线路端口加速
date: 2019-10-21 18:52:43
customizeurl: trojan-globalssh-port
categories:
- [科学上网, Trojan]
- [一键脚本]
tags:
- Trojan
- 一键脚本
img: /images/trojan.png
top: false
cover: false
coverImg: 
password: 
toc: true
mathjax: false
summary: 谷歌云搭建Trojan科学上网，使用GlobalSSH端口加速，优化Trojan科学上网端口速度
keywords: Trojan,一键脚本,GCP,Global SSH,Ucloud
---

Trojan+GlobalSSH+域名解析[Cloudflare]，延迟低稳定

## 准备工作

1.服务器

2.域名

3.Ucloud账户[需要实名]

## 域名解析

将你的域名解析一条A记录指向服务器IP

如图：

<img src="/images/2144089706.png" style="zoom:75%;" />

## 搭建Trojan

atrandys大佬的首发一键脚本

```
curl -O https://raw.githubusercontent.com/atrandys/trojan/master/trojan_mult.sh && chmod +x trojan_mult.sh && ./trojan_mult.sh
```

执行以上脚本，然后选择1，安装trojan，然后输入解析到VPS的域名，回车安装即可。

## 自愿安装bbr

建议安装bbr，来源于网络分享。

```
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

## 修改Trojan默认端口

```
vi /usr/src/trojan/server.conf
```

修改server.conf的"local_port": 443,字段即可。

重启：reboot

## 利用Ucloud的全球动态加速PathX的GlobalSSH加速你的Trojan端口[最后修改的端口]

进入[Ucloud的控制台的全球动态加速PathX的GlobalSSH的页面](https://console.ucloud.cn/upathx/globalssh)

点击创建

如图：

<img src="/images/2144089707.png" style="zoom:75%;" />

确定之后创建完毕，生成一个形如：IP.ipssh.net的域名

## 再次回到域名解析

1.删除原来的A记录

2.新建CNAME记录指向IP.ipssh.net

如图：

<img src="/images/2144089708.png" style="zoom:75%;" />

等待生效，大概半小时连通

## 使用方法

填入域名，端口，密码，即可使用