# docker run

```bash
docker run -d --name mrdoc -p 10086:10086 -v ~/mrdoc:/app/MrDoc/config -v ~/mrdoc/media:/app/MrDoc/media jonnyan404/mrdoc-nginx

docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer

```


## apt换国内源

```bash

```

## docker换国内源

```bash
sudo nano /etc/docker/daemon.json
```

```bash
{
    "registry-mirrors": [
        "https://docker.m.daocloud.io", 
        "https://noohub.ru", 
        "https://huecker.io",
        "https://dockerhub.timeweb.cloud",
        "https://mirror.ccs.tencentyun.com",
        "https://registry.docker-cn.com",
        "http://docker.mirrors.ustc.edu.cn",
        "http://hub-mirror.c.163.com"
    ]
}
```