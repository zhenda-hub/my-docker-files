```yaml
# yt-dlp 配置解释版（伪 YAML 格式）

cookiefile: /cookies/cookies.txt              # 登录 cookie，用于下载需要认证的视频（如 B 站、会员内容）
add_metadata: true                            # 启用视频元数据嵌入（作者、ID、标题等）

writesubtitles: true                          # 下载字幕（人工上传字幕）
writeautomaticsub: true                       # 下载自动生成字幕（如 YouTube 自动识别字幕）
subtitleslangs:                               # 下载以下语言的字幕（去掉直播弹幕）
  - zh
  - en
  - "-live_chat"
subtitlesformat: srt                          # 字幕格式设为 .srt
embedsubtitles: false                         # 不嵌入字幕（使用外挂字幕）

updatetime: false                             # 禁止修改文件时间戳，保留真实下载时间
writethumbnail: true                          # 下载视频封面图
writeinfojson: true                           # 下载视频元信息文件（.info.json）
restrictfilenames: true                       # 限制文件名字符，避免空格/特殊符号

postprocessors:                               # 下载后处理步骤
  - key: Exec
    exec_cmd: chmod 0664                      # 修改下载文件权限
    when: after_move                          # 下载后修改
  - key: FFmpegEmbedSubtitle
    already_have_subtitle: false              # FFmpeg 插件：嵌入字幕（此项即便设置了，但 embedsubtitles=false，会忽略）
  - key: FFmpegMetadata
    add_chapters: true                        # 添加章节信息（如果源视频中有）

```