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





能力	是否可实现
多清晰度转码	✅ 可以，手动或实时转码
自适应播放	✅ Jellyfin 有部分 ABR 能力，但体验不如 YouTube
CDN 支持	❌ 没有全球节点，只有你本地的设备
兼容性优化	✅ 但需要一定的配置和硬件（如硬件加速）



转码（Transcoding） = 把视频的“编码格式 / 分辨率 / 码率”转为设备更容易播放的形式。
结果：占用带宽更低，兼容性更好，播放更流畅！



Jellyfin 硬件加速配置
1. 检查硬件支持
```bash
# 检查集成显卡设备
ls -la /dev/dri/
# 应该能看到类似 renderD128 的设备

# 查看显卡信息
lspci | grep VGA
# 或
sudo lshw -c display
```
1. Docker 配置（推荐）
```yaml
# docker-compose.yml
version: "3.8"
services:
  jellyfin:
    image: jellyfin/jellyfin:latest
    container_name: jellyfin
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Shanghai
    volumes:
      - ./config:/config
      - ./cache:/cache
      - /path/to/your/videos:/media
    ports:
      - "8096:8096"
    # 关键：映射GPU设备
    devices:
      - /dev/dri/renderD128:/dev/dri/renderD128
      - /dev/dri/card0:/dev/dri/card0
    restart: unless-stopped
```

1. Jellyfin 内部设置
访问 http://your-nas-ip:8096，进入管理界面：

Intel Quick Sync Video (QSV)：专门用于视频编解码加速

管理 → 转码 → 硬件加速：
✅ 启用硬件解码：选择 "Video Acceleration API (VAAPI)"
✅ 启用硬件编码：选择 "Video Acceleration API (VAAPI)"
✅ 硬件解码选择：H264, HEVC, VP9
✅ 硬件编码选择：H264, HEVC
性能优化配置
1. 系统级优化
```bash
# 确保用户在render组中
sudo usermod -a -G render $USER

# 检查GPU权限
ls -la /dev/dri/
# 应该显示render组权限
```

2. 针对N150的转码设置
```json
// Jellyfin 转码设置建议
{
  "EnableHardwareDecoding": true,
  "HardwareDecodingCodecs": ["h264", "hevc", "vp9"],
  "EnableHardwareEncoding": true,
  "HardwareEncodingCodecs": ["h264", "hevc"],
  "H264Crf": 23,          // 质量设置：23是较好的平衡点
  "MaxMuxingQueueSize": 2048,
  "EnableThrottling": false,
  "EnableSegmentDeletion": true
}
```
3. 内存和缓存优化
```yaml
# docker-compose.yml 添加内存限制
services:
  jellyfin:
    deploy:
      resources:
        limits:
          memory: 2G      # N150配置通常内存有限
        reservations:
          memory: 512M
    # 使用SSD作为转码缓存目录
    volumes:
      - /path/to/ssd:/config/transcodes  # 临时转码文件
      - /path/to/hdd:/media             # 媒体库
```


```bash
# 安装 VAAPI 支持库
sudo apt install libva-glx2 libva-drm2 libva-x11-2 libva-dev
#  检查 VAAPI 驱动是否安装成功
vainfo
```



启用硬件转码

检查 VAAPI 是否生效：

1. 登录 Jellyfin Web 后台
2. 播放 4K 视频 → 点“管理面板”（右上角）
3. 查看 播放信息：
- 显示为 Direct Play → 说明未转码
- 显示为 Transcode (VAAPI) → ✅ 成功启用
- 显示为 Transcode (ffmpeg) → ❌ 仍用软件转码


```yaml
devices:
  - /dev/dri:/dev/dri

```
HandBrake 开启预转码, 不要实时转码

```bash

# iPerf, 在NAS和播放设备间测试带宽
iperf3 -s  # NAS上运行服务端
iperf3 -c nas-ip

```


Chrome或Edge，并启用硬件加速（浏览器设置 > 系统 > 使用硬件加速）。

增加缓存大小（设置 > 高级 > 缓存），确保视频预加载更多数据。





3️⃣ 配置高级转码参数
在 “转码” 页面中可以设置以下：

参数	设置建议
最大转码视频分辨率	可设为 1080p（防止强制 4K）
转码 H.264 编码器	软件（libx264）或硬件加速
转码封装格式（容器）	MP4
码率限制	720p: 3Mbps，1080p: 6~8Mbps，4K: 15Mbps
音频编码格式	AAC（兼容手机和浏览器）



🔄 三、强制使用“直接播放”优先（避免频繁转码）
在每个用户的“播放设置”中：

复制
编辑
用户 → 播放设置 → 直接播放优先级
设置：

✅ 启用直接播放

✅ 启用直接流式播放（Direct Stream）

✅ 禁用转码（或设为“仅限必要时”）




 
由于致命的播放器错误，播放失败。 FFmpeg exited with code 187