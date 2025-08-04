# 家庭 NAS 快速开始指南

> 面向 NAS 初学者和爱好者的入门级教程，帮助你快速理解、选型、搭建和使用家庭 NAS，构建属于自己的数据中心。

---

## 🛒 1. 硬件准备

### ✅ 推荐设备类型

| 类型              | 说明                        | 适合人群      |
| --------------- | ------------------------- | --------- |
| 品牌 NAS（群晖、威联通等） | 系统成熟，界面友好                 | 小白用户      |
| 迷你主机 + 自建系统     | 成本低，可玩性高（如 GMK、Intel NUC） | DIY 爱好者   |
| 老电脑 / 树莓派       | 利旧方案                      | 极客 / 预算有限 |

### ✅ 硬盘建议

* 使用 NAS 专用硬盘（如 WD Red / Seagate IronWolf）
* 推荐容量：4TB 起步；多个盘组成 RAID（建议至少 2 盘）
* 注意供电与散热：稳定运行是关键

---

## 🧰 2. 系统安装与选型

### 📦 常见 NAS 操作系统

| 系统                       | 特点                     | 适合人群     |
| ------------------------ | ---------------------- | -------- |
| **群晖 DSM**               | 界面优秀，功能强大              | 入门 & 商用  |
| **Unraid**               | 插件丰富，支持 Docker/KVM 虚拟化 | 玩机中阶     |
| **OpenMediaVault (OMV)** | 开源免费，基于 Debian         | Linux 用户 |
| **TrueNAS SCALE**        | 企业级开源系统                | 高级用户     |

> 💡 自建用户推荐 OMV（上手快）或 Unraid（更灵活）

---

## ⚙️ 3. 基本功能配置

### 📁 文件服务

* 启用 SMB/NFS/FTP，适配各类终端访问
* 创建共享文件夹（如 Photos, Videos, Docs）
* 设定用户权限：按需开放读写

### 🔐 远程访问

* 使用 Tailscale / Zerotier 实现安全远程连接（比直接公网暴露安全）
* 或通过 VPN 接入家中局域网

### 🛡️ 安全建议

* 禁用默认 admin 账户，启用强密码 + 2FA
* 不轻易开放 5000/22/80 等常见端口到公网
* 定期更新系统和容器镜像

---

## 🐳 4. 容器化服务推荐（Docker）

在 NAS 上运行 Docker，可部署各种轻量服务：

| 服务                  | 功能                       |
| ------------------- | ------------------------ |
| **FileBrowser**     | 网页文件管理器                  |
| **Immich**          | 智能照片图库（替代 Google Photos） |
| **MeTube**          | YouTube 下载器              |
| **Plex / Jellyfin** | 媒体服务器                    |
| **AdGuard Home**    | 局域网广告拦截                  |
| **Portainer**       | 图形化 Docker 管理界面          |

> 推荐使用 `docker-compose` 管理服务配置，便于备份与重建

---

## 🧩 5. 日常使用建议

* 📱 使用手机 App（如 DS File、Tailscale、Jellyfin）访问 NAS
* 🧠 构建标签式数据分类体系：例如 `照片/家庭/2023-旅行`
* ⏱️ 自动备份手机照片、微信文件等重要数据到 NAS
* 🔁 使用定时脚本或工具实现自动同步 & 备份

---

## 📚 延伸阅读

* [家庭 NAS 数据备份指南](./nas_backup_guide.md)
* [家庭 NAS 安全指南](./nas_security_guide.md)
* [immich：开源 AI 照片系统](https://github.com/immich-app/immich)
* [OpenMediaVault 官方](https://www.openmediavault.org/)
* [Unraid Wiki](https://wiki.unraid.net/UnRAID_6/Manual)
* [Docker 中文手册](https://yeasy.gitbook.io/docker_practice/)

---

## ✅ 总结

* NAS = 私人云 + 数据中枢 + 应用平台
* 建议从文件存储 & 自动备份开始，逐步拓展多媒体与服务部署
* 安全与稳定优先，建议每月维护和备份一次

> 用 NAS 守护你的数字生活，用数据记录家庭的每一个瞬间。

---

*版本：2025-08*
