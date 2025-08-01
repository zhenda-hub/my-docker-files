# 🧾 FileBrowser 使用指南

![FileBrowser Logo](https://via.placeholder.com/800x300.png?text=FileBrowser)  
*轻量级 Web 文件管理器*

---

## 📄 什么是 FileBrowser?

> FileBrowser 是一个轻量级 Web 文件管理器，支持文件添加、编辑、管理、预览、分享、用户权限管理等功能，可定制化级别高，适合自定义 NAS 环境。


### 🌟 核心功能

- **Web 界面**：通过浏览器管理本地/远程文件  
- **权限控制**：支持用户/组权限管理  
- **文件操作**：上传、下载、重命名、删除、压缩  
- **API 支持**：通过 REST API 集成自动化任务  
- **多平台部署**：Linux、Docker、Windows 一键运行  


### 🔍 常见使用场景

| 场景      | 解释                   |
| ------- | -------------------- |
| 私有文件网盘  | 自定义文件分类，应用于照片、文档、电影等 |
| 交流文件    | 通过网页分享链接，方便小组或远程访问   |
| 家庭公共文件夹 | 设置公共账号访问家庭共用资源       |
| 进阶用户管理  | 给不同用户设置不同规则和正则       |


---

## 🛀 部署方式

### Docker 部署

使用 docker-compose 部署：

```yaml
services:
  filebrowser:
    image: filebrowser/filebrowser
    container_name: filebrowser
    user: "$UID:$GID"
    volumes:
      - /your/files:/srv
      - ./filebrowser/config:/config
    ports:
      - 8080:80
    restart: unless-stopped
```

运行后：

* Web 访问地址： `http://localhost:8080`
* 默认账号: `admin` / `admin`

---


<!-- ## 🐛 常见问题 -->
## ❗ 常见问题


??? question "无法访问Web界面"
    **可能原因**: 端口被占用或防火墙阻止
    
    **解决方案**:
    ```bash
    # 检查端口占用
    netstat -tlnp | grep 8080
    
    # 检查防火墙状态
    sudo ufw status
    
    # 检查服务状态
    systemctl status filebrowser
    ```

??? question "文件上传失败"
    **可能原因**: 权限不足或磁盘空间不够
    
    **解决方案**:
    ```bash
    # 检查磁盘空间
    df -h
    
    # 检查目录权限
    ls -la /path/to/files
    
    # 修改权限
    sudo chown -R filebrowser:filebrowser /path/to/files
    ```

---

## 📚 扩展资源

- **官方网站**: [https://filebrowser.org](https://filebrowser.org)
- **GitHub仓库**: [https://github.com/filebrowser/filebrowser](https://github.com/filebrowser/filebrowser)
- **文档中心**: [https://filebrowser.org/docs](https://filebrowser.org/docs)
- **演示站点**: [https://demo.filebrowser.org](https://demo.filebrowser.org)
