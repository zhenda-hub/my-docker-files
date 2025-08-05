```bash
# Docker安装
docker run -d \
  --name duplicati \
  -p 8200:8200 \
  -v /volume1/duplicati:/config \
  -v /volume1:/source \
  duplicati/duplicati
```
# 特点
- 支持AES-256加密
- 增量备份
- 支持多种云存储后端
- Web界面管理