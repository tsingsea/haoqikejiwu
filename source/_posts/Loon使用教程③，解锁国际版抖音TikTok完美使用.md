---
title: Loon使用教程③，解锁国际版抖音TikTok完美使用
date: 2020-04-29 17:20:35
customizeurl: loon-unlock-tiktok
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
mathjax: false
summary: 
keywords: Loon,iOS,配置文件,TikTok,抖音,国际版抖音
---

<img src="/images/216253459.gif" style="zoom: 50%;" />

## Loon 解锁 TikTok 区域限制

在`[URL Rewrite]`字段下添加如下代码

```
(?<=_region=)CN(?=&) KR 307
(?<=&app_version=)16..(?=.?.?&) 1 307
(?<=\?version_code=)16..(?=.?.?&) 1 307
```

区域请修改下方国家代码，默认为韩国`KR`。