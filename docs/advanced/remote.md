# 家庭 NAS 远程访问指南

> 本文为 NAS 爱好者提供一个安全、稳定、高效的家庭 NAS 远程访问解决方案，帮助你在外也能轻松访问家中 NAS 上的文件、照片、多媒体等内容。

---

## 🌐 什么是远程访问 NAS？

远程访问指的是：在外网环境（如手机 4G、公用 WiFi、异地电脑）下，通过网络访问部署在家中的 NAS 设备，实现：

* 文件访问与上传
* 多媒体播放（电影、照片、音乐）
* 远程管理（如 Docker 容器、系统后台）

> ⚠️ 远程访问 ≠ 暴露 NAS 到公网，请优先考虑 **安全通道**

---

## ✅ 常见远程访问方式对比

| 方式                           | 是否推荐  | 优点        | 风险               |
| ---------------------------- | ----- | --------- | ---------------- |
| 公网端口转发（如开放 5000）             | ❌ 不推荐 | 简单快速      | 高暴露风险，容易被扫描攻击    |
| ZeroTier / Tailscale 虚拟局域网   | ✅ 推荐  | 安全、易用、免费  | 依赖第三方服务          |
| VPN（OpenVPN / WireGuard）     | ✅ 推荐  | 可控性强、兼容性好 | 需额外配置            |
| DDNS + 反向代理（Nginx / Traefik） | ⚠️ 中阶 | 灵活、自定义域名  | 需 HTTPS 配置与防火墙规则 |

---

## 🧰 方式一：使用 Tailscale 快速访问 NAS

### 步骤

1. 注册 [Tailscale 账号](https://tailscale.com)
2. 在 NAS 上安装 Tailscale（支持群晖 / Unraid / OMV / Linux）
3. 在手机、笔记本等设备也安装 Tailscale 并登录同一账户
4. 在外网环境下直接访问 NAS 局域网 IP（如 `192.168.1.100:8000`）

### 优点

* 安装简单，免端口转发
* 自动加密，点对点传输
* 可与 ACL 配合做设备访问限制

---

## 🧩 方式二：自建 VPN（如 WireGuard）

### 步骤简述

1. 在路由器或 NAS 上部署 WireGuard 服务端
2. 配置 NAT 端口转发（通常为 51820）
3. 在客户端设备上导入配置文件连接

### 推荐工具

* 群晖用户：可用套件中心中的 VPN Server + WireGuard
* OpenWRT 路由器用户：安装 `luci-app-wireguard`
* Docker 用户：`linuxserver/wireguard` 镜像

---

## 🌍 方式三：DDNS + HTTPS + 反向代理

适用于需要使用域名访问 NAS 服务（如 immich.jacknas.com）

### 组件

* DDNS：将动态 IP 映射为固定域名（Cloudflare / 阿里云 DDNS）
* 反向代理：通过 Nginx / Traefik 转发不同端口到子服务
* HTTPS：使用 Let's Encrypt 自动申请免费证书

### 示例服务组合

| 服务          | 子域名            | 示例                       |
| ----------- | -------------- | ------------------------ |
| FileBrowser | file.nas.com   | `https://file.nas.com`   |
| Immich      | photos.nas.com | `https://photos.nas.com` |
| Portainer   | docker.nas.com | `https://docker.nas.com` |

> ⚠️ 需做好防火墙控制与 Fail2Ban 限制访问

---

## 🖥️ 常见远程访问场景

| 目标          | 推荐方案                             |
| ----------- | -------------------------------- |
| 在外访问文件      | Tailscale / WebDAV + HTTPS       |
| 上传照片        | Immich 客户端（通过 Tailscale 或 HTTPS） |
| 远程下载任务      | Aria2 + FileBrowser，通过反代或 VPN    |
| 远程管理 Docker | Tailscale + Portainer 登录         |
| 家人访问媒体库     | Jellyfin / Plex + HTTPS 域名接入     |

---

## 🔐 安全建议

* 禁用默认账户，开启强密码和 2FA
* 所有 Web 服务使用 HTTPS，避免明文登录泄露密码
* 定期更新 NAS、Docker 镜像、反代证书
* 配置 Fail2Ban / CrowdSec 防暴力破解
* 建议结合防火墙 + GeoIP 限制国外或异常 IP 访问

---

## 📱 移动端工具推荐

| 工具                           | 功能            |
| ---------------------------- | ------------- |
| **Tailscale App**            | 虚拟内网访问 NAS    |
| **DS File / FileBrowser**    | 管理文件          |
| **Immich App**               | 自动上传手机照片到 NAS |
| **Jellyfin / Infuse / Plex** | 远程观看视频        |
| **Termius**                  | SSH 登录管理      |

---

## ✅ 总结

* **推荐方式：Tailscale + HTTPS 服务反代**，兼顾易用与安全
* **不建议直接暴露公网端口**，尤其是 22、5000、80、443 等默认端口
* **为不同服务分配子域名与单独端口，提高安全隔离性**
* 配置好远程访问后，建议用备用手机/网络测试外部可用性与速度

> 一个安全的远程访问系统，将是你 NAS 最有价值的能力之一。

---

## 📚 延伸阅读

* Tailscale 官方文档: [https://tailscale.com/kb/](https://tailscale.com/kb/)
* WireGuard 官网:     [https://www.wireguard.com/](https://www.wireguard.com/)
* openvpn文档:        [https://openvpn.net/community-docs/index.html?lang=en/](https://openvpn.net/community-docs/index.html?lang=en/)
* Cloudflare DDNS 教程: [https://developers.cloudflare.com](https://developers.cloudflare.com)
* Nginx Proxy Manager: [https://nginxproxymanager.com/](https://nginxproxymanager.com/)
* [家庭 NAS 安全指南](./security.md)
