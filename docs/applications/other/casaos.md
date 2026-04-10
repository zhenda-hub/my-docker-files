
## 常用命令
```bash
# Quick Setup CasaOS
wget -qO- https://get.casaos.io | sudo bash
# Update CasaOS
wget -qO- https://get.casaos.io/update | sudo bash
# Uninstall CasaOS
casaos-uninstall
```

<https://github.com/IceWhaleTech/CasaOS>


```bash
# look compose files
ll /var/lib/casaos/apps

# 数据存储位置
/DATA/AppData/
/DATA/
```

### reset pw

```bash
ls /var/lib/casaos/db/user.db
sudo mv /var/lib/casaos/db/user.db /var/lib/casaos/db/user.db.backup
sudo systemctl restart casaos-user-service.service
```

## 坑


旧应用程序 (待重建)

docker run d app

immich-postgres is unhealthy


## 使用心得

不要让它接管现有容器.会破坏容器

把它当应用市场使用即可
