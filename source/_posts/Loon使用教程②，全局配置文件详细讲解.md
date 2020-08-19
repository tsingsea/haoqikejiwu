---
title: Loon使用教程②，全局配置文件详细讲解
date: 2020-03-19 17:19:07
customizeurl: loon-config
categories:
- [iOS, Loon]
tags:
- iOS
- Loon
img: /images/Loon.png
top: false
cover: false
coverImg: 
password: 
toc: true
keywords: Loon,iOS,配置文件,Global
description: Loon配置文件详细教程
---

成文不易，此文没有[官方](https://www.notion.so/Loon-f0a98c39f5224c09b281c79837380431)详细，但改动都清晰可见，按照顺序很容易理解，对小白极其友好！

------

## 一、示例配置文件赏析

### 商店版

```
#default configure
#Update Date: 2019-10-21 11:42:20 +0000
#author: Loon

[General]
skip-proxy = 192.168.0.0/16,10.0.0.0/8,172.16.0.0/12,localhost,*.local,e.crashlynatics.com
bypass-tun = 10.0.0.0/8,100.64.0.0/10,127.0.0.0/8,169.254.0.0/16,172.16.0.0/12,192.0.0.0/24,192.0.2.0/24,192.88.99.0/24,192.168.0.0/16,198.18.0.0/15,198.51.100.0/24,203.0.113.0/24,224.0.0.0/4,255.255.255.255/32
# [DNS] => DNS 服务器
dns-server = system,119.29.29.29,223.5.5.5
allow-udp-proxy = false
host = 127.0.0.1


[Proxy]
# 内置 DIRECT、REJECT 策略
# 节点名称 = 协议，服务器地址，服务器端口，加密协议，密码，
1 = Shadowsocks, 1.2.3.4, 443, aes-128-gcm, "password"
2 = Shadowsocks, 1.2.3.4, 443, aes-128-gcm, "password"
3 = ShadowsocksR, 1.2.3.4, 443, aes-256-cfb,"password",auth_aes128_md5,{},tls1.2_ticket_auth,{}
4 = ShadowsocksR, 1.2.3.4, 10076, aes-128-cfb,"password",auth_aes128_md5,{},tls1.2_ticket_auth,{}
# vmess
# 节点名称 = 协议，服务器地址，端口，加密方式，UUID，传输方式:(tcp/ws),path：websocket握手header中的path，host：websocket握手header中的path，over-tls:是否tls，tls-name：远端w服务器域名，skip-cert-verify：是否跳过证书校验（默认否）
#5 = vmess, 1.2.3.4, 10086, aes-128-gcm,"uuid",transport:ws,path:/,host:icloud.com,over-tls:true,tls-name:youtTlsServerName.com,skip-cert-verify:false

[Remote Proxy]
# 订阅节点
# 别名 = 订阅URL
Subs = https://example/server-complete.txt
Subs2 = https://example2/server-complete.txt

[Remote Filter]
# 筛选订阅节点，筛选后的结果可加入到策略组中，目前支持三种筛选方式
# NodeSelect: 使用在UI上选择的节点。
# NameKeyword: 根据提供的关键词对订阅中所有节点的名称进行筛选，使用筛选后的节点。
# NameRegex: 根据提供的正则表达式对订阅中所有节点的名称进行筛选，使用筛选后的节点。
Netflix = NodeSelect,Subs
Hulu = NameKeyword,Subs,Subs2,FilterKey = Hulu
HK = NameRegex,Subs,FilterKey = *HK

[Proxy Group]
# 节点选项
PROXY = select,Auto,1,2,3,4,Subs
# url-test模式，给提供的url发出http header请求，根据返回结果，选择测速最快的节点，默认间隔600s，测速超时时间5s，为了避免资源浪费，建议节点数不要过多，只支持单个节点和远端节点，其他会被忽略
Auto = url-test,1,2,3,4,Subs,url = http://bing.com/,interval = 600
# fallback模式，和url-test类似，不同的是会根据顺序返回第一个可用的节点，为了避免资源浪费，建议节点数不要过多，只支持单个节点和远端节点，其他会被忽略
Auto1 = fallback,1,2,3,4,Subs,url = http://bing.com/,interval = 600
# 别名 = ssid，默认 = 策略， 蜂窝 = 策略， ssid名称 = 策略
SSID = ssid, default = PROXY, cellular = DIRECT, "DivineEngine" = PROXY
# 广告模式
Advertising = select,REJECT,DIRECT
# 白名单模式 PROXY，黑名单模式 DIRECT
Final = select,PROXY,DIRECT

[Rule]
# Local RULE
# Type:DOMAIN-SUFFIX,DOMAIN,DOMAIN-KEYWORD,USER-AGENT,URL-REGEX,IP-CIDR
# Strategy:DIRECT,Proxy,REJECT
# Options:force-remote-dns(Default:false),no-resolve
DOMAIN,google.com,PROXY
# GeoIP China
GEOIP,CN,DIRECT
FINAL,Final

[Remote Rule]
# Remote Rule
# 订阅规则URL,策略
# PROXY
https://raw.githubusercontent.com/Loon0x00/LoonExampleConfig/master/Rule/ExampleRule.list,PROXY

[URL Rewrite]
enable = true
# Redirect Google Search Service
^https?:\/\/(www.)?(g|google)\.cn https://www.google.com 302

[Remote Rewrite]
# 订阅 URL Rewrite
# 订阅url,别名(可选)
https://raw.githubusercontent.com/Loon0x00/LoonExampleConfig/master/Rewrite/AutoRewrite_Example.list,auto

[MITM]
hostname = *.example.com,*.sample.com
enable = true
skip-server-cert-verify = true
#ca-p12 =
#ca-passphrase =
```

### TF版本v-2.1.0

【商店版基础上增加脚本配置模块】

```
[Script]
enable = true
# http-request 处理请求的脚本
# http-response 处理请求响应的脚本
# cron 定时脚本

# http-request ^https?:\/\/(www.)?(example)\.com script-path=localscript.js
# http-response ^https?:\/\/(www.)?(example)\.com script-path=https://example.com/loon.js,timeout=10,requires-body = true
# cron "0 8 * * *" script-path=cron.js
```

------

## 二、配置文件各版块通讲

### 1、[General]

默认不做修改

### 2、[DNS]

```
dns-server字段后面可增加你认为优质的dns
allow-udp-proxy字段可以开启关闭udp模式
host字段本机不做修改
```

##### eg：

```
dns-server = system,119.29.29.29,223.5.5.5,1.1.1.1,8.8.8.8,114.114.114.114,8.8.4.4
allow-udp-proxy = true
host = 127.0.0.1
```

### 3、[Proxy]

此板块通过配置文件书写单个节点，但是Loon比Quantumult X有着友好的ui添加ss ssr v2ray节点，故不用再此处修改，如果你有自己的vps搭建的专属节点，你可以放在配置文件，更新配置文件即包含节点，无需每次更新后在ui界面再次添加，根据实际情况节省时间与精力。

### 4、[Remote Proxy]

此板块为远程订阅节点，如果机场多的朋友，强烈建议在此添加链接。通过ui添加浪费时间。

##### 书写语法

```
订阅名称 = 订阅链接
Subs = https://example/server-complete.txt
```

##### eg：[好奇科技坞v2ray节点视频](https://www.youtube.com/watch?v=6ffFMBAvRyQ&t)，[好奇科技坞v2ray节点博客](https://seaseax.com/curious-v2ray.html)

```
好奇科技坞-禁止转载分享 = https://*******
```

### 5、[Remote Filter]

节点筛选，此板块稍微复杂，但是很实用。

### 6、[Proxy Group]

策略组版块，策略类型四种：select，url-test，fallback，SSID，根据这四种基本类型，增加强大的策略组。

##### eg：若想复制使用，请配和下边的8、[Remote Rule]，因为有关联。

```
PROXY = select,好奇科技坞-禁止转载分享
Auto = select,url-test,好奇科技坞-禁止转载分享,url = http://bing.com/,interval = 600
Auto1 = select,fallback,好奇科技坞-禁止转载分享,url = http://bing.com/,interval = 600
SSID = ssid, default = PROXY, cellular = DIRECT, "DivineEngine" = PROXY
Global = select,PROXY,Auto,Auto1
YouTube = select,PROXY,Auto,Auto1
Netflix = select,PROXY,Auto,Auto1
Advertising = select,PROXY,Auto,Auto1
Telegram = select,PROXY,Auto,Auto1
Apple = select,PROXY,Auto,Auto1
China = select,DIRECT
```

### 7、[Rule]

此板块ui添加友好

### 8、[Remote Rule]

远程分类规则，此板块建议配置文件放好，与[Proxy Group]配合使用。

```
https://raw.githubusercontent.com/Loon0x00/LoonExampleConfig/master/Rule/ExampleRule.list,PROXY
```

##### eg：若想复制使用，请配和上边的6、[Proxy Group]，因为有关联。

```
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Unbreak.list, policy=DIRECT, tag=Unbreak, enable=true
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Advertising.list, policy=Advertising, tag=Advertising, enable=true
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Hijacking.list, policy=Advertising, tag=Hijacking, enable=true
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Media/YouTube.list, policy=YouTube, tag=YouTube, enable=true
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Media/Netflix.list, policy=Netflix, tag=Netflix, enable=true
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Media/HBO.list, policy=Global, tag=HBO, enable=true
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Media/Fox.list, policy=Global, tag=Fox, enable=true
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/GlobalMedia.list, policy=Global, tag=GlobalMedia, enable=true
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/HKMTMedia.list, policy=Global, tag=HKMTMedia, enable=true
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Telegram.list, policy=Telegram, tag=Telegram, enable=true
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Global.list, policy=Global, tag=Global, enable=true
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Apple.list, policy=Apple, tag=Apple, enable=true
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/China.list, policy=China, tag=China, enable=true
```

### 9、[URL Rewrite]

默认不动，如有需要可ui添加。

### 10、[Remote Rewrite]

##### eg：官方复写没有放入hostname，所以我把hostname和Rewrite整合在我的仓库新建一个链接，方便使用。

```
https://raw.githubusercontent.com/ssooenftzero/0X/master/Loon/conf/loonnowshremoterewrite.conf, tag=官方复写好奇整合, enable=true
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Rewrite.conf, tag=神机复写, enable=true
```

### 11、[Script]

~~此板块商店版暂无。所以此块eg代码适用于tf版本。~~

伴随着商店版的更新，Loon即将迎来了一波涨价，Loon将支持真正意义上的远程调用js脚本，大家且用且珍惜，Quantumult X作者也是在一拨人滥用脚本之后，狠心阉割远程脚本功能，不希望Loon迎来这样的局面，因为远程给我们省下了很多事儿。

##### eg：此脚本远程连接，几乎整合所有大佬的js，所以无需再次重复添加

```
#nzw9314整理
https://raw.githubusercontent.com/nzw9314/Loon/master/Script.conf
https://raw.githubusercontent.com/nzw9314/Loon/master/Cookie.conf
https://raw.githubusercontent.com/nzw9314/Loon/master/Task.conf
```

### 12、[MITM]

证书版块，此板块也不需要动，因为10、[Remote Rewrite]的远程订阅已经包含需要的hostname字段。证书在ui界面生成安装。