# Glances：NAS 爱好者的系统监控利器

## 简介

**Glances** 是一个跨平台的系统监控工具，适用于 Linux、macOS、Windows 等环境。它以终端界面为主，也可以通过 Web 界面进行远程监控。对于 NAS 爱好者来说，Glances 提供了一种轻量、直观的方式来实时查看系统资源使用情况。

如果你在运行 Docker、部署各种自托管服务，或者只是想了解 NAS 的运行状态，Glances 都是一个非常实用的工具。

---

## 核心功能

* 🖥️ **CPU 监控**：实时显示 CPU 使用率、核心负载情况。
* 💾 **内存监控**：展示总内存、已用、缓存、swap 等。
* 📀 **磁盘监控**：磁盘 I/O、容量使用情况。
* 🌐 **网络监控**：流量速率、网络接口信息。
* 📦 **进程监控**：可排序查看消耗资源最多的进程。
* 🐳 **容器监控**：支持 Docker 容器的资源使用情况（需安装扩展）。
* 📊 **Web 界面**：提供 REST API 与 Web UI，便于远程查看。

---

## 安装方式

### Ubuntu / Debian

```bash
sudo apt update
sudo apt install glances -y
```

### Python pip 安装（推荐）

```bash
pip install glances
```

### Docker 部署

```bash
docker run -d \
  --name=glances \
  -p 61208-61209:61208-61209 \
  --pid host \
  -v /var/run/docker.sock:/var/run/docker.sock:ro \
  nicolargo/glances:latest-full
```

部署后访问：

```
http://服务器IP:61208
```

即可使用 Web 界面。

---

## 常用命令

* 启动 Glances（终端模式）：

  ```bash
  glances
  ```
* 以 Web 服务器模式运行（默认端口 61208）：

  ```bash
  glances -w
  ```
* 查看帮助：

  ```bash
  glances -h
  ```

---

## 适合人群

* ✅ 使用 NAS 的家庭用户，想要轻量化监控工具。
* ✅ 自托管玩家，运行 Docker、数据库等服务，需要随时关注资源。
* ✅ 想要一站式监控 CPU、内存、磁盘、网络的系统管理员。

---

## 优势与不足

**优势：**

* 部署简单，依赖少。
* 界面直观，信息全面。
* 支持 Web UI 和 REST API，扩展性好。
* 跨平台，适合不同环境的 NAS 用户。

**不足：**

* 界面基于终端，初学者可能觉得信息过载。
* 不如 Grafana/Prometheus 那样支持复杂可视化和长时间数据存储。

---

## 总结

Glances 是一款非常适合 NAS 爱好者的 **系统资源监控工具**。
它既能轻量运行在终端中，又能通过 Web UI 提供远程监控能力，是自托管爱好者必备的“小帮手”。 🚀

如果你希望随时掌握 NAS 的运行状况，而又不想部署过于复杂的监控系统，Glances 值得一试。
