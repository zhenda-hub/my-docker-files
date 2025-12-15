# my-docker-files

docker应用百宝箱， 包括 docker配置和相关文档

```txt
为nas爱好者,写一个 xxxx文档. 以可复制的markdown文件输出. 放进 MkDocs 博客
```

## mkdocs init

<https://squidfunk.github.io/mkdocs-material/>

```bash
# create
mkdocs new .

mkdocs new mk-demo/
cd mk-demo/

# dev
mkdocs serve --help
mkdocs serve -a localhost:8989

# build
mkdocs build
```

### mkdocs plugins

- mkdocs-git-revision-date-localized-plugin: 自动显示文档最后修改时间（基于 Git 提交记录），支持格式自定义（如 YYYY-MM-DD）
- mkdocs-statistics-plugin: 生成字数、代码块数、阅读时间等统计信息（适合做分析 / 页面报告）
- mkdocs-glightbox: 图片、视频、iframe 的现代化灯箱展示
- mkdocs-video: 便捷嵌入视频
- mkdocs-minify-plugin: 对“首屏加载 + 传输体积”的提升通常在 10%～40% 区间
- mkdocs-encryptcontent-plugin: 页面加密
- mkdocs-macros: 利用变量和宏



## 设备项目位置统计

- ubunutu
~/Documents/docker_ws/cloudreve_demo
~/Documents/docker_ws/immich-app

- windows
F:\ME2\docker_ws