---
title: Trojan首发一键搭建脚本
date: 2019-09-30 09:22:27
customizeurl: trojan-install-sh
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
summary: 使用免费300额度的谷歌云搭建Trojan科学上网，本脚本应该算是Trojan首发一键脚本
keywords: Trojan,一键脚本,GCP,谷歌云实例
---

## 谷歌云搭建Trojan科学上网

### 创建实例

详情请跟着[视频教程](https://www.youtube.com/watch?v=d3Xk_vHERE0)做

### SSH连接实例

### Trojan一键脚本

开启TLS1.3，系统支持centos7+/debian9+/ubuntu16+

```
wget -N --no-check-certificate -q -O trojan_install.sh "https://raw.githubusercontent.com/V2RaySSR/Trojan/master/trojan_install.sh" && chmod +x trojan_install.sh && bash trojan_install.sh
```

以上代码执行完毕，窗口显示一串下载链接，复制以上链接到浏览器下载即可，可能需要扶墙。

### 安装bbr加速，建议锐速。

- 第一次执行脚本安装锐速

```
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

- 第二次执行脚本开启锐速

```
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

### 搭建完成

愉快的使用Trojan吧！！！

### 附加

trojan服务端修改密码

```
vi /usr/src/trojan/server.conf
```

修改完成后，重启trojan服务端即可，同时客户端的密码也要同步修改

```
systemctl restart trojan
```
