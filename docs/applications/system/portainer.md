# Portainer：NAS 爱好者的容器管理面板

## 简介

**Portainer** 是一个轻量级的开源容器管理面板，专为 Docker、Kubernetes 等容器环境设计。它通过直观的 Web 界面，让用户能够轻松管理容器、镜像、网络和卷。对于 NAS 爱好者来说，Portainer 是一个理想的选择，可以帮助你快速部署和管理自托管服务。

如果你不想频繁使用命令行管理 Docker，Portainer 能显著提升体验和效率。

---

## 核心功能

* 🐳 **容器管理**：创建、启动、停止、删除和查看容器日志。
* 📦 **镜像管理**：拉取、构建、删除镜像。
* 🌐 **网络管理**：查看和配置 Docker 网络。
* 💾 **卷管理**：管理数据卷，持久化存储。
* 👥 **用户与访问控制**：支持多用户和基于角色的访问权限。
* ⚙️ **应用模板**：一键部署常见应用（如 Nextcloud、Jellyfin、WordPress）。
* 🚀 **支持多环境**：不仅支持本地 Docker，还能管理远程 Docker、Swarm、Kubernetes。

---

## 部署方式

### Docker Compose 部署

```yaml
version: '3.3'

services:
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    restart: always
    ports:
      - "9000:9000"
      - "9443:9443"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - portainer_data:/data

volumes:
  portainer_data:
```

部署步骤：

1. 将上面的 `docker-compose.yml` 保存到服务器。
2. 运行 `docker compose up -d`。
3. 打开浏览器访问 `http://服务器IP:9000`。
4. 设置管理员账号并登录。

---

## 常用功能演示

* **查看容器日志**：在 Web 界面点击容器 → Logs。
* **进入容器控制台**：点击容器 → Console，即可进入交互式终端。
* **部署应用模板**：点击 App Templates，一键安装常见服务。
* **创建新容器**：填写镜像名、端口映射、卷挂载，即可快速启动。

---

## 适合人群

* ✅ 想要用 Web 界面管理 Docker 的 NAS 爱好者。
* ✅ 不熟悉命令行，但想尝试自托管服务的用户。
* ✅ 需要集中管理多个 Docker 主机的进阶玩家。

---

## 优势与不足

**优势：**

* 界面友好，操作直观，降低学习成本。
* 功能覆盖 Docker 日常管理需求。
* 支持多环境（本地 / 远程 / Kubernetes）。
* 活跃的社区和持续更新。

**不足：**

* 高级功能（Portainer Business Edition）需要付费。
* 相比命令行，灵活性稍差。
* 在低性能设备上，Web 界面可能略显卡顿。

---

## 扩展资源

* 🌐 [Portainer 官方网站](https://www.portainer.io/)
* 📖 [Portainer 文档](https://docs.portainer.io/)
* 💬 [Portainer GitHub 仓库](https://github.com/portainer/portainer)
* 📰 [NAS 社区对 Portainer 的讨论（Reddit r/selfhosted）](https://www.reddit.com/r/selfhosted/)
* 🎥 [Portainer 入门视频教程（YouTube）](https://www.youtube.com/results?search_query=portainer+tutorial)

---

## 总结

Portainer 是一款非常适合 NAS 爱好者的 **容器管理工具**。
它简化了 Docker 的管理流程，让你无需深入命令行就能轻松掌控自托管应用的部署与运行。 🚀

如果你希望让 NAS 的容器管理更高效、更直观，Portainer 是一个值得尝试的利器。
