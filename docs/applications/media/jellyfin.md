# Jellyfin 使用指南：为 NAS 爱好者打造的媒体中心

> 本文是面向家庭 NAS 用户的 Jellyfin 入门与实践指南，帮助你快速搭建本地媒体中心，畅享高质量观影体验。

---

## 📘 介绍

[Jellyfin](https://jellyfin.org/) 是一个 100% 免费、开源、无广告的媒体服务器，支持视频、音乐、图片等内容的索引、分类与播放。

* 支持多种客户端（网页、手机、智能电视、Kodi）
* 支持多用户管理、媒体元数据刮削、字幕下载
* 替代 Emby / Plex 的最佳选择
* 社区活跃、插件丰富、持续更新

Jellyfin 可完美运行于家庭 NAS 中，是打造私有影音平台的首选方案。

---

## 🐳 Docker 部署

推荐使用 Docker 部署，配置灵活、更新简单，适合主流 NAS 系统（如 Unraid、群晖、TrueNAS、Ubuntu Server）。

### 步骤一：准备目录结构

```bash
mkdir -p ~/jellyfin/config
mkdir -p ~/jellyfin/cache
mkdir -p ~/jellyfin/media
```

### 步骤二：编写 `docker-compose.yml`

```yaml
version: "3.8"
services:
  jellyfin:
    image: jellyfin/jellyfin
    container_name: jellyfin
    network_mode: host
    volumes:
      - ./config:/config
      - ./cache:/cache
      - ./media:/media
    restart: unless-stopped
```

> 使用 `network_mode: host` 可简化远程访问配置。

### 步骤三：启动服务

```bash
docker compose up -d
```

默认访问地址：http\://NAS\_IP:8096/

---

## 📚 相关知识点

### ✅ 媒体命名规范（刮削成功关键）

* 电影：`电影名 (年份).mp4`
* 电视剧：`剧名/Season 01/剧名 - S01E01.mkv`

推荐工具：

* [FileBot](https://www.filebot.net/)
* [tinyMediaManager](https://www.tinymediamanager.org/)

### ✅ 媒体分类建议

```bash
/media
├── Movies
│   └── Interstellar (2014).mp4
├── TV Shows
│   └── The Office
│       └── Season 01
│           └── The Office - S01E01.mkv
└── Music
    └── Artist/Album/track01.mp3
```

### ✅ 硬件转码支持

如你播放高码率 4K HEVC 视频，建议开启转码：

* Intel CPU：Quick Sync Video
* NVIDIA GPU：支持 NVENC
* AMD GPU：部分支持 VAAPI

设置路径：**管理后台 → 播放 → 硬件加速设置**

---

## ❓ 常见问题解答（FAQ）

### Q1: 视频播放卡顿？

* 检查是否启用硬件转码
* 视频码率过高？建议提前转码（如 4K → 1080p，HEVC → H.264）
* 局域网网速不够？建议使用千兆网口与有线连接

### Q2: 刮削失败？中文电影不识别？

* 命名不规范，请参照推荐格式
* 修改语言与元数据语言设置为简体中文
* 启用 OpenSubtitles 插件下载字幕

### Q3: 如何远程访问 Jellyfin？

* 使用 Tailscale / Zerotier 实现内网穿透
* 或搭配 Nginx + Cloudflare Tunnel 实现安全公网访问

### Q4: Jellyfin 和 Emby / Plex 有什么区别？

| 特性    | Jellyfin | Emby   | Plex     |
| ----- | -------- | ------ | -------- |
| 是否开源  | ✅ 是      | ❌ 否    | ❌ 否      |
| 是否免费  | ✅ 完全免费   | ❌ 部分收费 | ❌ 高级功能收费 |
| 插件生态  | ⭐⭐       | ⭐⭐⭐    | ⭐⭐⭐⭐     |
| 多平台支持 | ✅        | ✅      | ✅        |


由于致命的播放器错误，播放失败。 FFmpeg exited with code 187

手机流畅播放 需要转码

---

## 🔗 扩展资源推荐

* 官方网站：[https://jellyfin.org](https://jellyfin.org)
* 中文文档：[https://jellyfin.org/docs/general/](https://jellyfin.org/docs/general/)
* GitHub 源码：[https://github.com/jellyfin/jellyfin](https://github.com/jellyfin/jellyfin)
* 推荐插件：

  * `Jellyfin MetaData`：改进元数据刮削
  * `Jellyfin Plugin Repositories`：第三方插件源
  * `AniDB / OpenSubtitles`：动漫 / 字幕支持

---



TODO:
错误记录






转码（Transcoding） = 把视频的“编码格式 / 分辨率 / 码率”转为设备更容易播放的形式。
结果：占用带宽更低，兼容性更好，播放更流畅！


硬件加速配置


1. 安装gpu驱动
2. 查看驱动组的id
3. gpu驱动绑定到容器
4. 给compose文件添加驱动组， 获得访问权限



```bash
# 查看是否支持硬件解码
ls /dev/dri

```

```bash

# 检查GPU权限
ls -la /dev/dri/
# 应该显示render组权限


# 查询组id
getent group render | cut -d: -f3
getent group video | cut -d: -f3
getent group input | cut -d: -f3

sudo usermod -aG video jellyfin
sudo usermod -aG render jellyfin  # 将 Jellyfin 用户加入 render 组


```





- <https://jellyfin.org/docs/general/post-install/transcoding/hardware-acceleration/intel/#configure-with-linux-virtualization>
- <https://dgpu-docs.intel.com/driver/client/overview.html>
