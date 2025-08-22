# Calibre + Calibre-Web 文档

适合 **NAS 爱好者** 使用的 Calibre + Calibre-Web 部署与使用指南。

---

## 简介

* **Calibre**：功能强大的电子书管理工具，支持几乎所有电子书格式。
* **Calibre-Web**：Calibre 的 Web 前端，提供浏览器访问、在线阅读和远程管理功能。

搭配 NAS，可以实现：

* 家庭私有电子书管理系统
* 在线阅读（手机 / 平板 / 电脑）
* 支持分类、标签、搜索
* 远程访问和共享

---

## 功能特点

* 支持多种电子书格式（EPUB, MOBI, PDF 等）
* 在线阅读 & 下载
* 分类、标签、作者、系列管理
* 多用户支持（可控权限）
* 与 OPDS 协议兼容，支持阅读器应用对接（如 KOReader, Marvin）

---

## 安装与部署

### Docker Compose 示例

```yaml
version: "3.8"

services:
  calibre:
    image: linuxserver/calibre
    container_name: calibre
    restart: unless-stopped
    volumes:
      - ./config/calibre:/config
      - ./books:/books
    ports:
      - "8080:8080"

  calibre-web:
    image: linuxserver/calibre-web
    container_name: calibre-web
    restart: unless-stopped
    depends_on:
      - calibre
    volumes:
      - ./config/calibre-web:/config
      - ./books:/books
    ports:
      - "8083:8083"
```

* `./books`：存放电子书的目录
* `./config/*`：配置文件存储目录

访问：

* Calibre: `http://NAS_IP:8080`
* Calibre-Web: `http://NAS_IP:8083`

---

## 使用技巧

* 上传书籍 → 使用 Calibre 桌面端批量管理
* Calibre-Web → 用来远程访问和阅读
* 标签和分类可以在 Calibre 中编辑好，再同步到 Web 端
* 支持从 Calibre-Web 直接推送到 Kindle（需要配置邮箱）

---

## 常见问题 (FAQ)

**Q: Calibre 和 Calibre-Web 有什么区别？**
A: Calibre 是桌面端管理工具，功能全面；Calibre-Web 是 Web 前端，专注远程访问和阅读。

**Q: 支持在线阅读吗？**
A: 支持。Calibre-Web 内置 EPUB、PDF 在线阅读器。

**Q: 能和手机电子书阅读器同步吗？**
A: 支持 OPDS 协议，常见阅读器都能接入。

---

## 扩展资源

* [Calibre 官方网站](https://calibre-ebook.com/)
* [Calibre-Web GitHub](https://github.com/janeczku/calibre-web)
* [LinuxServer.io 镜像文档](https://docs.linuxserver.io/images/docker-calibre)
* [zlibrary](https://zh.z-library.sk/)

---

📚 部署好 Calibre + Calibre-Web，你的 NAS 就能变身电子书服务器，实现全平台访问和阅读。
