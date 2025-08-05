# 家庭 NAS 高可用实现方案指南

> 本文旨在帮助 NAS 爱好者构建一个稳定、高可用的家庭 NAS 系统，避免因硬件或服务故障造成数据不可访问或丢失。

---

## 📘 介绍

家庭 NAS 通常承载着照片、视频、工作资料、媒体中心等多重任务，一旦 NAS 出现故障，影响范围会非常广。因此，引入高可用（High Availability, HA）机制对于保障家庭数据安全具有重要意义。

---

## 🧱 高可用的核心目标

* ✅ 服务不中断：NAS 系统崩溃或重启时，服务自动切换或快速恢复
* ✅ 数据不丢失：硬盘损坏或文件误删时，有副本可还原
* ✅ 远程可控：即使外出也能恢复或排查服务状态

---

## 🛠️ 实现方式总览

| 类别     | 实现方式                                | 说明             |
| ------ | ----------------------------------- | -------------- |
| 硬盘冗余   | RAID 1 / 5 / 6 / ZFS / Btrfs        | 硬盘层面的冗余与容错     |
| 多机热备   | 主从备份 + Keepalived                   | 实现两台 NAS 高可用接管 |
| 定时备份   | rsync / rclone / Borg / Duplicati   | 定期将数据备份至异地或云端  |
| 容器自动重启 | Docker + Watchtower / Healthcheck   | 保证服务恢复与更新      |
| UPS 支持 | 不间断电源 UPS + 通知系统                    | 防止意外断电损坏数据     |
| 状态监控   | Netdata / Prometheus + Alertmanager | 实时查看健康状况       |

---

## 🧩 推荐架构示例

### ✅ 单机高可用方案（适合大多数家庭）

* 文件系统使用 ZFS 或 Btrfs，支持快照与自动修复
* RAID 1 或 RAIDZ1：保证至少一个硬盘损坏时数据不丢
* Docker 部署 Jellyfin、FileBrowser、Portainer 等
* 使用 `Duplicati` + `rclone` 定期同步至 OneDrive / Google Drive
* 安装 `Netdata` 实时监控 CPU、硬盘、温度等状态

### ✅ 双机热备方案（高阶用户）

* 两台 NAS，主机运行主要服务，备机做数据同步
* 使用 `rsync` + `cron` 或 `Syncthing` 实时同步文件夹
* 配置 `Keepalived` 管理浮动 IP 实现主备切换
* 使用同一外接 UPS 供电 + 警告通知脚本

---

## 📦 工具建议与说明

| 工具/技术       | 用途                |
| ----------- | ----------------- |
| ZFS / Btrfs | 文件系统支持快照、校验、压缩    |
| rsync       | 本地/远程文件夹增量同步      |
| Duplicati   | 支持加密、增量、云端备份      |
| Watchtower  | 自动检测并更新 Docker 容器 |
| Netdata     | 可视化 NAS 状态监控      |
| UPS 通知脚本    | 停电时自动安全关机 + 邮件通知  |

---

## ❓ 常见问题解答

### Q: RAID 等于备份吗？

> ❌ 不是。RAID 只是在硬盘级别提供容错能力，不能防止误删、人为损坏、勒索病毒等，必须结合异地/云备份方案。

### Q: 家庭是否需要双机 HA？

> 对于摄影师/开发者等重度数据用户来说非常有价值。普通家庭用户使用“单机高可用 + 云端定时备份”方案已足够。

### Q: 高可用 NAS 会不会更耗电？

> 双机方案功耗略高，但可设定“备机休眠、主机故障时唤醒”机制，合理配置可兼顾安全与节能。

---

## 🔗 延伸阅读

* [ZFS 官网](https://openzfs.org/)
* [Syncthing 同步工具](https://syncthing.net/)
* [Duplicati 备份工具](https://www.duplicati.com/)
* [Netdata 状态监控](https://www.netdata.cloud/)
* [Keepalived 浮动 IP](https://www.keepalived.org/)
* [家庭 UPS 推荐型号（论坛）](https://www.reddit.com/r/homelab/)

---

> 拥有一个高可用的 NAS，不只是存储更可靠，也是对数字生活的保障。实践中可逐步完善，从“单机 + 定时备份”开始，逐步向“异地 + 云 + 多机高可用”演进。

> _高可用是体验：保证系统在故障时“还能用”_