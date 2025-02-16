# docker run

```bash
# =================sys=================
# glances
docker run -d --restart="always" -p 61208-61209:61208-61209 -e GLANCES_OPT="-w" -v /var/run/docker.sock:/var/run/docker.sock:ro --pid host nicolargo/glances:latest-full

# portainer

# # old
# docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
# # new
# docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest

sudo docker run -d -p 8000:8000 -p 9443:9443 -p 9000:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:2.21.5

# =================tools=================
# ollama cpu
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
# ollama gpu
docker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama

# mrdoc
docker run -d --name mrdoc -p 10086:10086 -v ~/mrdoc:/app/MrDoc/config -v ~/mrdoc/media:/app/MrDoc/media jonnyan404/mrdoc-nginx

# memos
docker run -d --name memos -p 5230:5230 -v ~/.memos/:/var/opt/memos neosmemo/memos:stable

# maxkb
docker run -d --name=maxkb -p 8080:8080 -v ./maxkb:/var/lib/postgresql/data -v ./python-packages:/opt/maxkb/app/sandbox/python-packages cr2.fit2cloud.com/1panel/maxkb

# ebook2audiobook
docker run -it --rm -p 7860:7860 --platform=linux/amd64 athomasson2/ebook2audiobook python app.py
```

<https://docs.portainer.io/start/upgrade/docker>
<https://docs.docker.com/build/builders/>
