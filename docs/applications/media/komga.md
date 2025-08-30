# 📚 Komga NAS 部署与使用指南

## 什么是 Komga？

Komga 是一款开源的自托管漫画和电子书管理工具，支持 Web 界面和 OPDS 协议。适合 NAS 用户集中管理漫画、小说、杂志、EPUB、PDF 等文件。

* 📖 支持格式：CBZ、CBR、ZIP、RAR、PDF、EPUB
* 🌐 Web 界面：通过浏览器随时访问
* 📱 移动支持：OPDS 适配阅读器（如 **KOReader**、**Moon+ Reader**）
* 🗂️ 分类清晰：支持按目录和标签组织

---

## 部署方式

### Docker Compose 部署

```yaml
version: "3.3"
services:
  komga:
    image: gotson/komga
    container_name: komga
    restart: unless-stopped
    ports:
      - "8080:8080"
    volumes:
      - /path/to/komga/config:/config
      - /path/to/komga/books:/books
```

说明：

* `/config` 👉 存放 Komga 配置与数据库
* `/books` 👉 存放漫画与电子书目录

启动：

```bash
docker compose up -d
```

---

## 目录结构示例

为了便于 Komga 扫描和分类，建议采用以下简化目录：

```plaintext
/books
  /Fiction        # 小说类
    Book1.epub
    Book2.mobi

  /Non-Fiction    # 散文、随笔
    Essay1.pdf

  /Biography      # 传记、回忆录
    PersonA.epub

  /History        # 历史类
    China.pdf

  /Philosophy     # 哲学思想
    Plato.epub
```

---

## 使用技巧

* **首次扫描**：放入书籍后，在 Komga Web 界面手动点击 `Scan Library`
* **自动扫描**：Komga 会定期检测新文件，也可在设置中调整频率
* **OPDS 接入**：打开阅读器 → 添加书源 → 输入 `http://<NAS-IP>:8080/opds`
* **标签与封面**：可以在 Web 界面中修改元数据、上传封面

---

## 常见问题

### 1. 扫描后没显示书籍？

* 确认书籍格式是否支持（EPUB、PDF、CBZ、CBR 等）
* 确认挂载的 `/books` 目录有读写权限
* 在 Web 界面手动点击 `Scan Library`

### 2. 书籍分类混乱？

* 建议按 **大类目录** 放书（如 Fiction / Non-Fiction）
* 避免一个目录下混放太多不同类型文件

### 3. 远程访问 NAS 上的 Komga？

* 配合 **反向代理**（如 Nginx Proxy Manager）
* 或使用 **Tailscale / Zerotier** 建立内网穿透

---

## 总结

Komga 非常适合 NAS 爱好者托管和分类电子书：

* 简单的目录结构即可良好运行
* 支持 Web 与移动设备访问
* 自动扫描更新，省心高效

> 📌 建议：小型书库可直接用 **三类分类（Fiction / Non-Fiction / Science）**，更简洁。
