---
title: v2ray官方教程过程全透明手动搭建v2ray(kcp)+shadowsocks(原生)双节点
date: 2020-08-21 09:01:55
customizeurl: v2core-v2ray-shadowsocks
categories:
- [科学上网, v2ray]
- [科学上网, shadowsocks]
- [Linux]
tags:
- v2ray
- shadowsocks
- Linux
description: 因v2ray原官方脚本已被v2fly接管，原官方脚本不在使用，新脚本复杂不友好，故按照原官方脚本整理出此教程，代码透明无后门。
---

## 注意事项

1. 支持系统不限，最好使用`CentOS`；`Debian`；`Ubuntu`常见发行版
2. 请提前开放你所需要用的端口
3. 涉及到的命令出现未安装情况，自行安装

## 详细教程

### 第一步

```
wget https://github.com/v2ray/v2ray-core/releases/download/v4.27.0/v2ray-linux-64.zip   //下载v2ray最新发行包，可自行替换版本号

unzip v2ray-linux-64.zip   //解压

cd v2ray-linux-64   //根据解压目录的具体情况决定是否运行本命令

ls -l   //列出解压后所有文件
```

### 移动文件

因为~~`bash <(curl -L -s https://install.direct/go.sh)`~~脚本会自动安装以下文件：

- `/usr/bin/v2ray/v2ray`：V2Ray 程序
- `/usr/bin/v2ray/v2ctl`：V2Ray 工具
- `/usr/bin/v2ray/geoip.dat`：IP 数据文件
- `/usr/bin/v2ray/geosite.dat`：域名数据文件
- `/etc/v2ray/config.json`：配置文件

于是现在要做的就是手动将文件移动至相应位置:

```
mkdir /usr/bin/v2ray   //在/usr/bin目录下创建v2ray文件夹
cp v2ray /usr/bin/v2ray/v2ray
cp v2ctl /usr/bin/v2ray/v2ctl
cp geoip.dat /usr/bin/v2ray/geoip.dat
cp geosite.dat /usr/bin/v2ray/geosite.dat
```

### 配置文件

无配置不成"方圆"

```
mkdir /etc/v2ray   //在/etc目录下创建v2ray文件夹
nano /etc/v2ray/config.json
```

v2ray(kcp)+shadowsocks(原生)配置文件模板

模板解释：

- v2ray mKCP协议
- alterID=32
- v2ray 默认端口：46231且动态端口范围40000-50000
- 默认uuid：0084dfc8-507e-715a-e797-15fa69d84321
- ss 默认端口：443
- 加密方式：chacha20-ietf-poly1305
- 默认密码：shadowsocks
- udp开启

可直接替换：

- 端口号
- alterID
- UUID
- 加密方式

```
{
    "log": {
        "access": "/var/log/v2ray/access.log",
        "error": "/var/log/v2ray/error.log",
        "loglevel": "warning"
    },
    "inbound": {
        "port": 46231,
        "protocol": "vmess",
        "settings": {
            "clients": [
                {
                    "id": "0084dfc8-507e-715a-e797-15fa69d84321",
                    "level": 1,
                    "alterId": 32
                }
            ]
        },
        "streamSettings": {
            "network": "kcp"
        },
        "detour": {
            "to": "vmess-detour-151377"
        }
    },
    "outbound": {
        "protocol": "freedom",
        "settings": {}
    },
    "inboundDetour": [
        {
            "protocol": "vmess",
            "port": "40000-50000",
            "tag": "vmess-detour-151377",
            "settings": {},
            "allocate": {
                "strategy": "random",
                "concurrency": 5,
                "refresh": 5
            },
            "streamSettings": {
                "network": "kcp"
            }
        },
        {
            "protocol": "shadowsocks",
            "port": 443,
            "settings": {
                "method": "chacha20-ietf-poly1305",
                "password": "shadowsocks",
                "udp": true,
                "level": 1
            }
        }
    ],
    "outboundDetour": [
        {
            "protocol": "blackhole",
            "settings": {},
            "tag": "blocked"
        }
    ],
    "routing": {
        "strategy": "rules",
        "settings": {
            "rules": [
                {
                    "type": "field",
                    "ip": [
                        "0.0.0.0/8",
                        "10.0.0.0/8",
                        "100.64.0.0/10",
                        "127.0.0.0/8",
                        "169.254.0.0/16",
                        "172.16.0.0/12",
                        "192.0.0.0/24",
                        "192.0.2.0/24",
                        "192.168.0.0/16",
                        "198.18.0.0/15",
                        "198.51.100.0/24",
                        "203.0.113.0/24",
                        "::1/128",
                        "fc00::/7",
                        "fe80::/10"
                    ],
                    "outboundTag": "blocked"
                }
            ]
        }
    }
}
```

### v2ray服务主程序

将v2ray.service文件移动到/usr/lib/systemd/system目录,生成V2Ray服务

```
mkdir /usr/lib/systemd/system   //在/usr/lib/systemd目录下创建system文件夹
cp ./systemd/v2ray.service /usr/lib/systemd/system
```

### 日志文件

手动创建一些文件,用于V2Ray程序运行时使用

```
mkdir /var/log/v2ray   //在/var/log目录下创建v2ray文件夹
touch /var/log/v2ray/access.log
touch /var/log/v2ray/error.log
touch /var/run/v2ray.pid
```

### 随系统自启

```
systemctl enable v2ray
```

### 管理命令

```
systemctl start v2ray
systemctl stop v2ray
systemctl status v2ray
```