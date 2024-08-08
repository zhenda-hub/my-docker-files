# docker run

```bash
# mrdoc
docker run -d --name mrdoc -p 10086:10086 -v ~/mrdoc:/app/MrDoc/config -v ~/mrdoc/media:/app/MrDoc/media jonnyan404/mrdoc-nginx

# portainer
# old
docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
# new
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest

# ollama cpu
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
# ollama gpu
docker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

<https://docs.portainer.io/start/upgrade/docker>
<https://docs.docker.com/build/builders/>


## windows docker 占用内存过大

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
