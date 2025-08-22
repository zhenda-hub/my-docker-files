# Calibre + Calibre-Web 部署指南（NAS爱好者版）

## 简介

在家庭 NAS 上管理电子书时，**Calibre + Calibre-Web** 是经典组合：

* **Calibre**：功能强大的电子书管理工具，用于本地整理、分类、编辑元数据、转换格式。
* **Calibre-Web**：轻量级 Web 前端，可通过浏览器访问 Calibre 库，支持搜索、在线阅读和下载。

## 部署架构

* **Calibre**：在本地电脑或 NAS 上运行，用于管理主库。
* **Calibre-Web**：以 Docker 容器运行，指向 Calibre 数据库目录，提供 Web UI。

## Docker Compose 示例

```yaml
docker-compose.yml

version: "3.8"
services:
  calibre-web:
    image: linuxserver/calibre-web
    container_name: calibre-web
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Shanghai
    volumes:
      - ./config:/config
      - ./books:/books
    ports:
      - 8083:8083
    restart: unless-stopped
```

* `./config`：Calibre-Web 配置目录
* `./books`：Calibre 数据库所在目录（需包含 `metadata.db`）
* Web UI 默认端口：`8083`

## Calibre 与 Calibre-Web 配合方式

1. 在 **Calibre 桌面应用**中添加书籍，生成 `metadata.db`。
2. 使用 Calibre 编辑元数据、生成封面、转换格式。
3. Calibre-Web 指向 `metadata.db` 所在目录，即可展示最新书库。

## 使用体验

* ✅ **Calibre**：适合本地批量管理和格式转换。
* ✅ **Calibre-Web**：适合家庭成员浏览、下载和在线阅读。
* 🚫 Calibre-Web **不具备编辑功能**（如修改元数据、转换格式），这些需在 Calibre 桌面端完成。

## 进阶玩法

* 搭配 **COPS** 或 **Komga**，提供更丰富的前端选择。
* 用 **Syncthing / Rclone / Nextcloud** 同步书库目录，实现多设备共享。
* 搭配 **Traefik / Nginx Proxy Manager** 实现 HTTPS 和外网访问。

## 总结

* **Calibre** = 强大本地管理
* **Calibre-Web** = 轻量 Web 访问

这一组合非常适合 NAS 爱好者：本地管理 + 网络访问，简单高效。
