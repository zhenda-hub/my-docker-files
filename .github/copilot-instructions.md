# Copilot Instructions for my-docker-files

本项目是一个 Docker 应用集合，提供了一系列预配置的自托管服务的 Docker Compose 配置文件。以下是关键信息，帮助 AI 助手理解和维护这个项目。

## 项目结构

```
my-docker-files/
├── cps-apps/          # 各个应用的 Docker Compose 配置
│   ├── aria2-pro/     # 下载工具
│   ├── immich-app/    # 照片管理
│   ├── jellyfin-app/  # 媒体服务器
│   └── ...
├── docs/              # MkDocs 文档
│   ├── applications/  # 应用指南
│   ├── advanced/      # 进阶配置
│   └── ...
└── mkdocs.yml        # MkDocs 配置文件
```

## 关键组件和模式

### Docker Compose 配置

- 所有应用配置位于 `cps-apps/` 目录下
- 每个应用独立的目录包含其 compose 文件 (`compose.yaml` 或 `docker-compose.yml`)
- 部分应用提供多个配置变体 (如 `compose.linux.yaml` 和 `compose.yaml`)

### 文档结构

- 使用 MkDocs Material 主题构建
- 文档按功能分类：系统工具、下载工具、媒体工具等
- 每个应用独立的 markdown 文件位于相应分类目录下

## 工作流程

### 添加新应用

1. 在 `cps-apps/` 创建新应用目录
2. 添加 Docker Compose 配置文件
3. 在 `docs/applications/` 相应分类下添加文档
4. 更新 `mkdocs.yml` 导航结构

### 文档更新

- 修改 `mkdocs.yml` 的 `nav` 部分添加新页面
- 文档使用中文编写
- 支持代码高亮、图表(Mermaid)等高级特性

## 关键文件示例

### Docker Compose 配置示例 (从 `jellyfin-app/compose.yaml`):
```yaml
services:
  jellyfin:
    container_name: jellyfin
    image: jellyfin/jellyfin:latest
    volumes:
      - ./config:/config
      - ./cache:/cache
      - /path/to/media:/media
```

### MkDocs 导航配置 (从 `mkdocs.yml`):
```yaml
nav:
  - 应用指南:
    - 媒体工具:
      - Jellyfin: applications/media/jellyfin.md
```

## 注意事项

- 所有应用配置需遵循 Docker Compose v3 规范
- 文档中的配置示例应包含必要的注释和说明
- 针对不同操作系统的特殊配置应单独说明

## 外部依赖

- Docker 和 Docker Compose
- Python 和 MkDocs（用于文档构建）
- Material for MkDocs 主题及其扩展

---

此指南将随项目发展持续更新。如发现任何不准确或需要补充的内容，请提出反馈。
