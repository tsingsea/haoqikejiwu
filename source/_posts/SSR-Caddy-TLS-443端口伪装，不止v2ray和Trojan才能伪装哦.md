---
title: SSR+Caddy+TLS+443端口伪装，不止v2ray和Trojan才能伪装哦
date: 2019-07-21 20:43:08
customizeurl: ssr-caddy-tls-443-sh
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
summary: 使用秋水大神的一键脚本进行ssr的安装，添加caddy+tls+443端口伪装，保证ssr应有速度的同时增加安全性。
keywords: shadowsocksr,一键脚本,秋水SSR,Caddy,tls加密
---

## 一，准备工作

1.服务器

2.域名

3.静态网页模板[下载](https://www.free-css.com/)

## 二，开始安装

Caddy[简介](https://zh.wikipedia.org/wiki/Caddy)一键安装脚本

```
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/caddy_install.sh && chmod +x caddy_install.sh && bash caddy_install.sh
```

## 三，域名解析

域名后台解析到服务器IP

## 四，域名注入

SSH客户端输入

```
cd /usr/local/caddy
```

查看/usr/local/caddy目录下有没有Caddyfile

```
echo "http://域名:80 {
redir https://域名:1234{url}
}
https://域名:1234 {
gzip
tls 邮箱
root /var/www/
redir https://域名{uri} 301
}" > /usr/local/caddy/Caddyfile
```

此段代码意思，直接新建Caddyfile文件并写入“引号内信息”

## 五，静态网页模板放置

1.在var/www/路径下放置网页

```
sftp手动放置
```

2.全命令操作（推荐）

```
cd /var

ls

wget https://www.free-css.com/assets/files/free-css-templates/download/page253/estateagency.zip

unzip estateagency.zip

mv 解压目录 www
```

3.其他caddy命令

```
启动：service caddy start
停止：service caddy stop
重启：service caddy restart
查看状态：service caddy status
查看Caddy启动日志： tail -f /tmp/caddy.log
Caddy配置文件位置：/usr/local/caddy/Caddyfile
```

4.测试访问，浏览器地址栏输入域名，看是否能够正常访问静态网页

## 六，SSR一键搭建脚本

```
wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
chmod +x shadowsocks-all.sh
./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
```

其他ssr命令

```
启动SSR：
/etc/init.d/shadowsocks-r start
退出SSR：
/etc/init.d/shadowsocks-r stop
重启SSR：
/etc/init.d/shadowsocks-r restart
SSR状态：
/etc/init.d/shadowsocks-r status
卸载SSR：
./shadowsocks-all.sh uninstall
```

更改ssr的相关配置参数，配置文件路径

```
/etc/shadowsocks-r/config.json
```

## 七，修改配置文件

```
vi /etc/shadowsocks-r/config.json
```

“server_port”: 端口改为443

```
eg:“server_port”:443,
```

"redirect": ["*:443#[127.0.0.1:前面caddy用到的端口]

```
eg:"redirect":["*:443#127.0.0.1:1234"],
```

重启SSR服务

```
/etc/init.d/shadowsocks-r restart
```

## 八，自愿安装bbr

```
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```