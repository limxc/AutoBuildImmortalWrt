# OrangePi 5 Plus 定制固件配置

> 基于 `Build 25.12.x Rockchip` 工作流定制
>
> Workflow: `.github/workflows/build-orangepi5plus-25.12.yml`
>
> 构建脚本: `rockchip/build25.sh`
>
> 插件配置: `shell/apk-custom-packages.sh`

---

## 默认参数

| 参数 | 原版 | 定制版 |
|------|------|--------|
| 机型 | `friendlyarm_nanopi-r3s` | `xunlong_orangepi-5-plus` |
| 管理地址 | `192.168.100.1` | `192.168.50.1` |
| 固件大小 | `1024 MB` | `2048 MB` |
| Store 商店 | `false` | `true` |
| Docker | `yes` | `yes` |
| PPPoE | `no` | `yes` |

---

## 插件清单

### 系统默认 (build25.sh)

| 插件 | 说明 |
|------|------|
| curl | HTTP 工具 |
| openssh-sftp-server | SFTP 支持 |
| luci-i18n-diskman-zh-cn | 磁盘管理 |
| luci-i18n-package-manager-zh-cn | 软件包管理 |
| luci-i18n-firewall-zh-cn | 防火墙 |
| luci-theme-argon | Argon 主题 |
| luci-app-argon-config | Argon 配置 |
| luci-i18n-argon-config-zh-cn | Argon 配置中文 |
| luci-i18n-ttyd-zh-cn | 网页终端 |
| luci-i18n-filemanager-zh-cn | 文件管理器 |

### 代理

| 插件 | 说明 |
|------|------|
| luci-app-openclash | OpenClash (clash.meta 内核) |
| luci-app-passwall2 + luci-i18n-passwall2-zh-cn | PassWall2 |
| luci-i18n-passwall-zh-cn | PassWall |
| xray-core / sing-box / hysteria / geoview | 代理依赖 |

### DNS / 去广告

| 插件 | 说明 |
|------|------|
| luci-app-adguardhome | AdGuardHome DNS 去广告 |
| luci-app-mosdns + luci-i18n-mosdns-zh-cn | MOSDNS 分流 |

### 网络

| 插件 | 说明 |
|------|------|
| luci-app-turboacc | Turbo ACC 网络加速 |
| luci-i18n-sqm-zh-cn | SQM QoS 队列管理 |
| luci-i18n-upnp-zh-cn | UPnP NAT 穿透 |
| luci-i18n-ddns-go-zh-cn | DDNS-GO 动态域名 |

### IPTV

| 插件 | 说明 |
|------|------|
| luci-i18n-msd_lite-zh-cn | 组播转 HTTP 流 |

### 工具

| 插件 | 说明 |
|------|------|
| bandix + luci-app-bandix + luci-i18n-bandix-zh-cn | 实时流量监控 |
| luci-i18n-wol-zh-cn | 网络唤醒 |
| luci-i18n-autoreboot-zh-cn | 定时重启 |
| luci-app-taskplan + luci-i18n-taskplan-zh-cn | 任务计划 |
| luci-app-partexp + luci-i18n-partexp-zh-cn | 分区扩容 |

### 界面 / 文件

| 插件 | 说明 |
|------|------|
| luci-i18n-quickstart-zh-cn | 首页向导 (含 istore) |
| luci-app-store | Store 商店 (workflow 注入) |
| luci-theme-aurora + luci-app-aurora-config | Aurora 极光主题 |
| bash quickfile luci-app-quickfile luci-i18n-quickfile-zh-cn | QuickFile 文件管理器 |
| luci-i18n-filebrowser-zh-cn | FileBrowser |

### Docker (workflow 参数控制)

| 插件 | 说明 |
|------|------|
| docker | Docker 引擎 |
| luci-i18n-dockerman-zh-cn | Docker 管理界面 |

---

## 使用方式

Fork 项目后，Actions → **Build OrangePi 5 Plus 25.12.x** → Run workflow，直接构建即可。

刷入 SD/eMMC 后，OrangePi 5 Plus 首次启动会自动：
- eth0 作为 WAN (PPPoE 拨号)
- eth1/eth2 作为 LAN (静态 IP `192.168.50.1`)
- WAN 入站放开，方便首次访问后台

---

## Sync Fork 后恢复

Sync fork 会覆盖以下文件的改动，需重新修改：

| 文件 | 修改内容 | 操作 |
|------|----------|------|
| `shell/apk-custom-packages.sh` | 插件开关 | 参照本文【插件清单】逐行取消注释/注释 |

以下文件 Sync 不会影响：

| 文件 | 原因 |
|------|------|
| `.github/workflows/build-orangepi5plus-25.12.yml` | 上游无此文件 |
| `orangepi5plus-config.md` | 上游无此文件 |
