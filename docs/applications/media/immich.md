# Immich：自托管的照片与视频备份方案

## 简介

**Immich** 是一个开源、自托管的照片与视频备份解决方案，专为家庭 NAS 爱好者和注重隐私的用户设计。它的目标是提供类似 Google Photos、iCloud Photos 的体验，同时让数据完全掌握在自己手里。

对于希望摆脱云厂商限制、追求数据可控的 NAS 玩家来说，Immich 是一个极佳的选择。

---

## 核心功能

* 📱 **自动备份**：支持 iOS 与 Android 客户端，拍摄的照片和视频可自动上传到服务器。
* 🌐 **Web 界面**：直观的浏览体验，支持相册、时间轴、地图视图。
* 👥 **多用户支持**：可为家人或朋友创建账号，集中管理全家人的照片。
* 🔍 **AI 功能**：

  * 人脸识别
  * 物体识别
  * 智能搜索（按人、地点、时间查找）
* 🗂️ **相册管理**：支持手动创建、分享和组织相册。
* 📍 **地理定位**：根据照片的 EXIF 信息在地图上显示拍摄位置。
* 🔒 **数据安全**：

  * 自托管，数据完全在本地。
  * 可结合 NAS 的 RAID、快照、备份方案，保证数据安全。

---

## 部署方式

Immich 官方推荐使用 **Docker Compose** 部署。下面是一个最小化示例：

```yaml
version: "3.9"

services:
  immich-server:
    image: ghcr.io/immich-app/immich-server:release
    container_name: immich_server
    restart: unless-stopped
    environment:
      - DB_HOST=immich_db
      - DB_PORT=5432
      - DB_USERNAME=postgres
      - DB_PASSWORD=postgres
      - DB_DATABASE_NAME=immich
    volumes:
      - ./upload:/usr/src/app/upload
    ports:
      - "2283:2283"
    depends_on:
      - immich_db

  immich_db:
    image: postgres:14
    container_name: immich_db
    restart: unless-stopped
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_DB=immich
    volumes:
      - ./pgdata:/var/lib/postgresql/data
```

部署步骤：

1. 将上面的 `docker-compose.yml` 保存到服务器。
2. 运行 `docker compose up -d`。
3. 打开浏览器访问 `http://服务器IP:2283`，初始化账号。
4. 下载手机端 App（App Store / Google Play 搜索 `Immich`），登录并启用自动备份。

---

## 适合人群

* ✅ 有 NAS / 服务器的用户
* ✅ 希望替代 Google Photos、iCloud 的用户
* ✅ 注重隐私与数据自主权的人
* ✅ 喜欢尝试新技术的自托管爱好者

---

## 优势与不足

**优势：**

* 完全开源，自托管，数据不依赖第三方。
* 功能快速迭代，社区活跃。
* 与现有家庭 NAS 生态高度兼容。

**不足：**

* 仍在快速开发中，可能存在小 bug。
* 部署需要一定的 Docker / Linux 基础。
* 资源占用较高（数据库、AI 功能需要 CPU/GPU）。

---


## 扩展资源

- 官网: [https://immich.app](https://immich.app)
- GitHub 仓库: [https://github.com/immich-app/immich](https://github.com/immich-app/immich)
- 文档: [https://immich.app/docs](https://immich.app/docs)

---

## 总结

Immich 为 NAS 爱好者提供了一个优秀的 **照片与视频集中管理方案**。
它不仅能替代云相册，还能与家庭 NAS 的存储与备份体系结合，真正做到 **“我的数据我做主”**。

如果你正打算构建一个属于自己的“家庭云”，Immich 值得一试。 🚀
