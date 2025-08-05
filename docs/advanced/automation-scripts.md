# 家庭 NAS 常用自动化脚本大全

> 本文为 NAS 爱好者整理常见自动化脚本示例，覆盖备份、同步、清理、镜像更新、通知等日常管理需求。脚本以 Bash / cron / Docker 命令为主，适用于 Linux、OMV、群晖等系统。

---

## 📁 目录结构

* 📦 1. 自动备份
* 🔄 2. 数据同步
* 🧹 3. 清理与归档
* 🐳 4. Docker 自动化
* 📮 5. 推送通知
* ⏰ 6. 定时任务设置

---

## 📦 1. 自动备份脚本

### 本地目录定时压缩备份

```bash
#!/bin/bash
src="/mnt/data/docs"
dest="/mnt/backup/docs_$(date +%F).tar.gz"
tar -czf "$dest" "$src"
```

### 使用 rclone 上传到 Google Drive

```bash
#!/bin/bash
rclone sync /mnt/data/photos gdrive:/nas_backup/photos -v --log-file=/var/log/rclone_photos.log
```

### Duplicacy CLI 增量加密备份

```bash
#!/bin/bash
cd /mnt/data/project1
duplicacy backup -stats -threads 4
```

---

## 🔄 2. 数据同步脚本

### 使用 rsync 同步本地两块盘数据

```bash
#!/bin/bash
rsync -a --delete /mnt/disk1/media/ /mnt/disk2/backup_media/
```

### 使用 Syncthing 自动同步两台设备

无需脚本，建议使用 Web UI 或 CLI 自动启动服务。

---

## 🧹 3. 清理与归档脚本

### 清理超过 30 天的临时文件

```bash
#!/bin/bash
find /mnt/temp -type f -mtime +30 -delete
```

### 自动归档旧照片至冷存目录

```bash
#!/bin/bash
src="/mnt/photos"
dest="/mnt/cold/photos_archive"
find "$src" -type f -mtime +180 -exec mv {} "$dest" \;
```

---

## 🐳 4. Docker 自动更新脚本

### Watchtower 替代脚本：检查并更新容器镜像

```bash
#!/bin/bash
containers=$(docker ps --format '{{.Names}}')
for c in $containers; do
  image=$(docker inspect --format='{{.Config.Image}}' $c)
  docker pull $image
  docker stop $c && docker rm $c
  docker run -d --name $c $image
  echo "$c 更新完成"
done
```

### 仅更新镜像（不重建容器）

```bash
#!/bin/bash
docker images --format '{{.Repository}}' | uniq | while read repo; do
  docker pull $repo
  echo "$repo 已更新"
done
```

---

## 📮 5. 推送通知脚本

### 发送推送通知到 Telegram

```bash
#!/bin/bash
BOT_TOKEN="your_bot_token"
CHAT_ID="your_chat_id"
MESSAGE="备份完成：$(date)"
curl -s -X POST https://api.telegram.org/bot$BOT_TOKEN/sendMessage \
  -d chat_id=$CHAT_ID \
  -d text="$MESSAGE"
```

### 通过 mail 命令发送本地邮件

```bash
#!/bin/bash
echo "系统备份已完成 $(date)" | mail -s "NAS备份通知" your@email.com
```

---

## ⏰ 6. 定时任务（cron）配置示例

### 编辑 crontab：

```bash
crontab -e
```

### 常见定时任务示例

```
# 每天凌晨 2 点备份照片到 Google Drive
0 2 * * * /opt/scripts/rclone_photos.sh

# 每周一清理临时目录
0 3 * * 1 /opt/scripts/clean_temp.sh

# 每日同步媒体数据
0 1 * * * /opt/scripts/rsync_media.sh
```

---

## ✅ 建议与实践

* 所有脚本统一放在 `/opt/scripts/`，并设为可执行：`chmod +x xxx.sh`
* 所有日志统一输出到 `/var/log/`，便于查看错误
* 高风险脚本（如删除）请加日志 & dry-run 模式
* 可用 systemd 定义服务，或容器内运行脚本调度器（如 cron + alpine）

---

## 📚 延伸阅读

* [Rclone 官方文档](https://rclone.org/docs/)
* [duplicacy CLI 文档](https://forum.duplicacy.com/c/cli/9)
* [Docker 自动更新指南](https://containrrr.dev/watchtower/)
* [crontab Guru](https://crontab.guru/)
* [Telegram Bot API](https://core.telegram.org/bots/api)

