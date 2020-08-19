---
title: 最简单的v2ray一键脚本
date: 2019-08-11 08:43:10
customizeurl: v2ray-233boy-sh
categories:
- [科学上网, v2ray]
- [一键脚本]
tags:
- v2ray
- 一键脚本
img: /images/v2ray.png
top: false
cover: false
coverImg: 
password: 
toc: true
mathjax: false
summary: 使用免费300额度的谷歌云搭建v2ray科学上网，最简单的搭建v2ray的一键脚本
keywords: v2ray,一键脚本,233boy脚本
---

### [视频教程](https://www.youtube.com/watch?v=aoMiqynu3fU)

### 准备工作

##### 1、服务器	

##### 2、域名

### 安装流程

##### 1、解析域名到服务器IP

##### 2、ssh终端执行一键代码

```
bash <(curl -s -L https://git.io/v2ray.sh) 
```

##### 3、终端填入解析好的域名，按步骤继续

##### 4、安装完成之后，检验域名能否访问伪装站，在浏览器地址栏输入域名查看是否有伪装站

##### 5、Cadddy管理命令（同4检查作用）

```
查看状态：service caddy status
```

### 自愿安装BBR

```shell
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```