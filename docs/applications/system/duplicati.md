# Duplicati 使用指南（面向 NAS 爱好者）

> 📦 本文档面向家庭 NAS 用户，介绍 Duplicati 的安装、配置、备份策略和常见问题，帮助你在家庭环境中实现高效安全的数据备份。

---

## 📌 什么是 Duplicati？

Duplicati 是一款开源的跨平台备份工具，支持增量备份、加密压缩、多种存储后端（包括本地路径、FTP、WebDAV、S3、OneDrive、Google Drive 等）。它通过 Web 界面管理任务，适合家庭用户和高级爱好者部署在 NAS 或 Docker 环境中。

官网：[https://www.duplicati.com](https://www.duplicati.com)

---
## 特点
- 支持AES-256加密
- 增量备份
- 支持多种云存储后端
- Web界面管理

---

## 🚀 安装方式

### ✅ 方式一：Docker 安装（推荐）

```yaml
version: '3.3'
services:
  duplicati:
    image: lscr.io/linuxserver/duplicati:latest
    container_name: duplicati
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Shanghai
    volumes:
      - /srv/docker/duplicati/config:/config
      - /mnt/backup:/backups
      - /mnt/nas:/source
    ports:
      - 8200:8200
    restart: unless-stopped
```

### ✅ 方式二：安装到系统中

* Linux：通过 `deb` 或 `rpm` 包安装
* Windows/Mac：官网下载对应安装包

---

## 🧠 基本概念

| 概念    | 说明                                      |
| ----- | --------------------------------------- |
| 源路径   | 被备份的数据，如 `/mnt/nas/photos`              |
| 目标路径  | 备份文件保存位置，如 `/mnt/backup` 或 Google Drive |
| 增量备份  | 仅备份变动的文件，提高效率                           |
| 加密/压缩 | 支持 AES-256 加密、压缩文件，保护数据隐私和节省空间          |
| 保留策略  | 可配置保留最近 N 天、N 个版本的备份，自动清理老备份            |

---

## 🛠 创建备份任务

1. 浏览器访问 `http://NAS-IP:8200`
2. 设置密码（推荐）
3. 点击“添加备份” > 选择高级模式
4. 配置：

   * 名称：`照片备份`
   * 源路径：如 `/source/photos`
   * 目标：如 `file:///backups/photos`
   * 加密：可开启
   * 计划：每天备份一次
   * 保留：保留最近 7 个版本
5. 保存并运行

---
## 设置远程访问
```bash
# 使用 nano 编辑配置文件
nano /etc/default/duplicati

# 把配置文件中的 DAEMON_OPTS 所在的行替换成下面这行内容。
# webservice-interface 参数为 any 表示任意接口都可以访问 duplicati 服务。
# webservice-port 参数为 8200，表示 Web 服务访问端口，如果需要改成其他端口，可以在这里修改。
DAEMON_OPTS="--webservice-interface=any --webservice-port=8200 --portable-mode"
```

---
## 🔁 自动化建议

* 使用 `duplicati` + `rclone` 实现“本地 + 云端”双重备份
* 本地不同磁盘备份 + 云盘(异地设备)备份

---

## 💬 常见问题

| 问题                | 解决方案                            |
| ----------------- | ------------------------------- |
| 如何还原数据？           | 进入 Web 界面 > 选择任务 > 还原           |
| 可以多个目录一起备份吗？      | 可以，将多个目录映射到 `/source/xxx`       |
| 备份文件太多，如何清理？      | 设置“保留策略”定期清除旧文件                 |
| 可以用 rclone 上传备份吗？ | 可以，用 rclone 定时同步 `/backups` 到云端 |
| 容器重启任务会丢失吗？       | 不会，只要 `/config` 卷正确挂载           |

---

## 🔗 扩展资源

* 官方文档：[https://duplicati.readthedocs.io](https://duplicati.readthedocs.io)
* 备份策略建议：[https://duplicati.readthedocs.io/en/latest/04-using-duplicati/03-backup-retention/](https://duplicati.readthedocs.io/en/latest/04-using-duplicati/03-backup-retention/)
* 社区论坛：[https://forum.duplicati.com](https://forum.duplicati.com)
- <https://hub.docker.com/r/linuxserver/duplicati>
- <https://docs.linuxserver.io/images/docker-duplicati/#ports-p>
- <https://docs.duplicati.com/detailed-descriptions/using-duplicati-from-docker>
- <https://docs.duplicati.com/getting-started/set-up-a-backup-in-the-ui#source-data>
- <https://nasdaddy.com/how-to-install-duplicati-on-your-nas/>

---

> ✅ 使用 Duplicati，你可以让家庭 NAS 的数据备份自动化、安全化、版本化，避免意外丢失带来的损失。




