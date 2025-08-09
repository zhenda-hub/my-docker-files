# docker run

```bash
# =================sys=================
# glances
docker run -d --restart="always" -p 61208-61209:61208-61209 -e GLANCES_OPT="-w" -v /var/run/docker.sock:/var/run/docker.sock:ro --pid host nicolargo/glances:latest-full
docker run -d --restart="always" -p 61208-61209:61208-61209 -e GLANCES_OPT="-w" -v /var/run/docker.sock:/var/run/docker.sock:ro -v /run/user/1000/podman/podman.sock:/run/user/1000/podman/podman.sock:ro --pid host nicolargo/glances:latest

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
docker run -d --name=maxkb -p 8080:8080 -v ~/maxkb:/var/lib/postgresql/data -v ~/python-packages:/opt/maxkb/app/sandbox/python-packages cr2.fit2cloud.com/1panel/maxkb

# ebook2audiobook
docker run -it --rm -p 7860:7860 --platform=linux/amd64 athomasson2/ebook2audiobook python app.py


# n8n

docker volume create n8n_data
docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n



# dify

# filebrowser

docker run \
    --name filebrowser \
    -v ~/Documents/ds_ws:/srv \
    -v ./filebrowser.db:/database/filebrowser.db \
    -v ./settings.json:/config/settings.json \
    -e PUID=$(id -u) \
    -e PGID=$(id -g) \
    -p 8888:80 \
    filebrowser/filebrowser
    # filebrowser/filebrowser:s6


# cinemore

docker run -d \
  --name cinemore-server \
  -p 8500:8000 \
  -v ./data:/app/data \
  -v ./media:/media \
  cinemore/cinemore-server:latest

# mediago 
docker run -d \
  --name mediago \
  -p 8899:8899 \
  -v ./mediago:/root/mediago \
  registry.cn-beijing.aliyuncs.com/caorushizi/mediago:v3.0.0

# dashy
docker run --name dashy -p 8098:8080 lissy93/dashy

# mp
docker run -d \
  --name moviepilot \
  -p 3000:3000 \
  -v ./config:/config \
  jxxghp/moviepilot-v2:latest


# speedtest
docker run -p 80:8080 -d --name speedtest ghcr.io/librespeed/speedtest
```




<https://docs.portainer.io/start/upgrade/docker>
<https://docs.docker.com/build/builders/>
