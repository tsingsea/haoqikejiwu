---
title: Loon使用教程①，软件上手详解
date: 2020-04-09 17:11:32
customizeurl: loon-use-mind
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
keywords: Loon,iOS,配置文件,mind,思维导图
---

### 成文时间：2020-04-09 17:11:32

### Loon[气球]

#### 概述

###### 简介：Loon是iOS平台上收费为2.99$的界面优美，操作方便的网络代理工具，***只是工具，不是VPN***。

###### 作者：[Twitter](https://twitter.com/loon0x00)；GitHub[库](https://github.com/Loon0x00/LoonManual)

###### 下载所需条件：①外区Apple ID；②外币支付方式。

### 界面介绍【思维导图】

#### Loon软件

<img src="/images/1987264126.png" style="zoom: 30%;" />

### 首页【仪表】从上到下

#### 第一版块

- 连接时间显示00:00:00
- 开关Start

#### 第二版块

- 添加【ss ssr vmess】
- 二维码扫描添加节点
- 订阅【订阅节点】
- 统计【统计速度及流量用量】
- 日志【观察运行状态】

#### 第三大版块【快捷方式】

- 模式选择

  - 全局直连【啥也不干】
  - 自动分流【常用：根据策略组干】
  - 全局代理【不常用：所有流量绕一圈】

- 策略组【四种类型】

  - Select

- 全局策略【两种模式】

  - Direct全局直连
  - Reject

- Final规则【内置】

  - DIRECT
  - REJECT

- 最近请求【主要查看你用网络干了啥】
- Rewrite
- MitM证书-高级功能必用
- 保存的请求-看你的爱好

### 配置-从上到下

#### 节点

- 单个节点管理
- 订阅节点管理
- 筛选节点-筛选订阅节点

  - NodeSelect:使用在UI.上选择的节点。
  - NameKeyword:根据提供的关键词对订阅中所有节点的名称进行筛选，使用筛选后的节点。
  - NameRegex:根据提供的正则表达式对订阅中所有节点的名称进行筛选，使用筛选后的节点。

#### 策略

#### 规则

- 单个规则-自己手动添加需要的规则
- 订阅规则-用远程链接订阅大佬的规则
- 规则测试-测试你的规则是否合理，速度影响等

#### Rewrite

- 手动书写重写规则
- 订阅大佬的重写规则

#### 脚本

- 因目前只有tf版，所以此模块单独讲

#### DNS

#### MITM

- 域名===Quantumult X上的hostname
- 安装证书

#### 编辑-老手编辑常用

- 手动操作，编辑功能强大，核心，可管理全局的编辑。

### 更多-从上到下

#### 设置

#### 帮助

#### 关于

### <img src="/images/1987264127.png" style="zoom: 50%;" />