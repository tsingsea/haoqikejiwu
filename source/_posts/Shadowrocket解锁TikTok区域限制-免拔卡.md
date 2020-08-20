---
title: Shadowrocket解锁TikTok区域限制-免拔卡
date: 2020-08-20 10:27:12
customizeurl: shadowrocket-unlock-tiktok
categories:
- [iOS, Shadowrocket]
tags:
- iOS
- Shadowrocket
- TikTok
description: " "
---

## 准备工作

1. 非大陆地区AppleID并已购买下载Shadowrocket，且是最新正版授权用户
2. 非大陆地区AppleID并已下载TikTok
3. 观看TikTok流量经过代理

## 视频教程

{% youtube 68pHg6fgv84 %}

## 详细教程

### 证书安装

1. 点击Shadowrocket首页底部**配置**
2. 选中一个配置文件，默认是`default.conf`
3. 弹出窗口点击**编辑配置**
4. `开启 HTTPS 解密` – `生成新的 CA证书` – `安装证书`

### 信任证书

1. 打开 `设置` – `通用` – `关于本机` – `证书信任设置` 
2. 找到`Shadowrocket开头的选项` – 打开右侧开关 – 弹出警告框 – `继续 - 信任证书即可

### 编辑配置

1. 点击Shadowrocket首页底部**配置**

2. 选中一个配置文件，默认是`default.conf`

3. 弹出窗口点击**编辑纯文本**

4. 找到`[URL Rewrite]`字段，在其下方

5. 复制并粘贴TikTok重写规则（URL Rewrite）代码：

   ```yml
   CN $1KR 302
   (?<=\?version_code=)16.. $11 302
   ```

6. 添加`hostname`，滑至末尾，复制并粘贴如下代码：

   ```
   hostname = *.tiktokv.com,*.musical.ly
   ```

### 更换区域

- 如果需要观看不同国家的TikTok视频，只需要修改[URL Rewrite]下方TikTok重写规则代码中的`KR`，将`KR`更换为其他国家的简码即可。