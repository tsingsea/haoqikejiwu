---
title: Quantumult X教程③，完美解锁TikTok教程
date: 2020-02-07 15:34:56
customizeurl: quantumultx-unlock-tiktok
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
keywords: Quantumult X,iOS,配置文件,TikTok,国际版抖音
---

iOS 使用解锁 TikTok （国际版）区域限制【Quantumult X 篇】

## 解锁Tiktok操作前必看

1.iMazing 备份TikTok，避免后续不小心更新Tiktok；

2.请使用正版圈x软件，如何查看正版，如下【绿色对勾为正版标识】：

<img src="/images/216253458.png" style="zoom:50%;" />

3.本人现在使用AppStore最新版tiktok(15.5.6)，仍能完美使用。

<img src="/images/216253459.png" style="zoom:50%;" />

## 详细步骤

### 使用Quantumult X 解锁 TikTok 区域限制

1.下载脚本配置文件，分别复制以下脚本配置文件链接

```
（NobyDa） https://raw.githubusercontent.com/NobyDa/Script/master/QuantumultX/Js.conf

（花姐） https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Rewrite.conf
```

2.进入QuantumultX，点击页面右下角三菱按钮，找到Rewrite模块，点击引用，粘贴刚刚复制的链接，右上角点击确定，点击全部同步就可以下载脚本配置文件

3.再次进入QuantumultX，点击页面右下角三菱按钮，找到配置文件-点击编辑-找到[rewrite_local]，并在下方粘贴以下代码；

```python
(?<=(carrier|sys)_region=)CN url 307 JP
(?<=version_code=)\d{1,}.\d{1}\.\d{1} url 307 14.0.0
```

### 美区为14.0.0，港区则将代码14.0.0改为8.4.0即可

1.复制api*.tiktokv.com, api*.musical.ly, api*.amemv.com, aweme*.snssdk.com，

2.进入QuantumultX，点击页面右下角三菱按钮，找到配置文件模块，点击编辑，滑至页面末尾；

3.（注意：在Rewrite模块引用的远程脚本配置文件js.con中包含了此项，所以这一步可以省略，大致明白原理即可）

4.找到[mitm]，在 hostname 后面粘贴，粘贴后效果大致如下：

```
hostname = api*.tiktokv.com, api*.musical.ly, api*.amemv.com, aweme*.snssdk.com
```

5.注意： ;hostname 前面的; 符号（注释符号），如果有这个符号，务必删掉；这一步其实跟Shadowrocket/Surge配置证书步骤等是一模一样的；在配置文件模块-编辑-下可以看到你所有配置的文本配置（即以文本样式进行配置），包括你的节点订阅，分流规则等等；

## 生成证书

1.进入QuantumultX，点击页面右下角三菱按钮，找到MinM模块，点击生成证书，提示生成成功，点击安装证书此时会跳转至 Safari，提示此网站...下载一个配置描述文件。您要允许吗？，点击允许，网页提示已下载描述文件；

2.进入 iOS 系统设置- 通用-描述文件-已下载的描述文件-选中，并安装，输入密码...完成描述文件安装；

3.进入 iOS 系统设置- 通用-关于本机-证书信任设置-针对根证书启用完全信任-选中刚刚安装的并启用即可；

## 享用Tiktok

<img src="/images/216253459.gif" style="zoom:50%;" />

1.进入QuantumultX，点击页面右下角三菱按钮

2.开启 Rewrite & MinM ；

## 换区操作

如想切换到其他地区，进入QuantumultX，点击页面右下角三菱按钮，找到Rewrite模块，点击添加，复制

```
(?<=(carrier|account|sys)_region=)CN url 307 JP
将JP修改成其他地区英文缩写即可，其他国家或地区代码。
```