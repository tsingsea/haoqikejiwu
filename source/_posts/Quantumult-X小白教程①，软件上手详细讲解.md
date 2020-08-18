---
title: Quantumult-X小白教程①，软件上手详细讲解
date: 2020-03-09 15:34:56
customizeurl: quantumultx-use-mind
categories:
- [iOS, Quantumult X]
tags:
- iOS
- Quantumult X
img: /images/Quantumult X.png
top: false
cover: false
coverImg: 
password: 
toc: true
mathjax: false
summary: 
keywords: Quantumult X,iOS,配置文件,Quantumult
---

## 软件简介：

1. 开发者：[Cross Utility](https://github.com/crossutility)

2. Quantumult X和Quantumult为同一开发者

3. 功能上，Quantumult X能用js脚本，但整体使用复杂

4. 附[超详细不完全教程](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917)，小白若是无耐心，劝你别看，你可能直接放弃！

## 软件布局概览：

App图标【还是挺酷】

<img src="/images/Quantumult X.png">

首次打开界面简单认识

<img src="/images/147035548.png" width="200" height="200">

主要操作界面简单认识

<img src="/images/147035549.png" height="200" width="200">

## 使用教程：

详细见[视频教程](https://www.youtube.com/watch?v=GI-cFrkXtIs)，此处仅仅列出需要用到的东西。

## 需要准备的东西：【从操作界面从上往下列出】

### 1.节点板块

UI界面添加节点只能添加ss/ss url/ss扫码添加，订阅链接需要转化为Quantumult X所支持的，网上各种转化接口，如下：

```
KOP-XIAO](https://github.com/KOP-XIAO/QuantumultX-Surge-API)：https://dove.589669.xyz/all2quanx?url=urlencode后的链接

[Fndroid](http://cloudcompute.lbyczf.com/x-rule-set[/github%E8%B7%AF%E5%BE%84])：http://cloudcompute.lbyczf.com/x-rule-set/“GitHub路径”

或者：http://cloudcompute.lbyczf.com/x-rule-set?url=普通订阅链接
```

针对小白，不介绍太多，此处不推荐在线转换，自行查找。

### 2.分流板块

手动添加分流，和shadowrocket Quantumult一样

引用-远程添加分流，附上简单list形式分流链接，感谢ConnersHua

```
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Unbreak.list				https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Advertising.list				https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Hijacking.list				https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/ForeignMedia.list				https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/DomesticMedia.list				https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/Global.list				https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Filter/China.list
```

搜索-主要用于你觉得哪条分流不对劲，用搜索功能查找修改/删除。

### 3.Rewrite重写板块

手动添加重写，小白请别想了，过。

引用-远程添加重写，附上简单conf形式重写链接，感谢ConnersHua

```
https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Rewrite.conf
```

搜索-主要用于你觉得哪条重写地址不对劲，用搜索功能查找修改/删除。

### 4.MitM证书板块

手动添加主机名，小白请别想了，不是很难，但没必要去手写。

1. 搜索-主要用于你觉得哪条hostname地址不对劲，用搜索功能查找修改/删除。

2. 生成证书，当你需要安装证书时，只需点击一下，然后点击配置证书，跳转safari浏览器，允许，设置-通用-描述文件-安装证书-关于本机信任证书

### 5.调试板块

1. 构造请求，此处点击，能看到所有利用脚本的定时任务，例如签到，比价，天气预报。例如京东每日获取cookies一次，在此处手动找到对应请求，执行一次，完成京东所有签到。

2. 调试记录，收藏，略过-基本不用

### 6.配置文件板块

1. 编辑-所有操作，最终的编辑处与体现处。

2. 导入-导入本地conf-此conf也包含所有配置

3. 导出-多用于备份，导出你满意的conf

4. 下载-远程下载conf-此conf也包含所有配置-例如我分享过的[Quantumult X配置文件讲解上](https://www.youtube.com/watch?v=ZCsUlLyfG-s)/[下](https://www.youtube.com/watch?v=L3zS-1k7M-4)

5. 实例-软件作者出场时给大家的模板，让大家参透。

6. 还原-跟你手机恢复出厂设置一个道理。

### 7.其他设置

点击进去，有白话文描述，自行查看

### 8.首页板块

细节操作描述不清,请看视频