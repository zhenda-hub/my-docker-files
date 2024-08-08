# docker run

```bash
# mrdoc
docker run -d --name mrdoc -p 10086:10086 -v ~/mrdoc:/app/MrDoc/config -v ~/mrdoc/media:/app/MrDoc/media jonnyan404/mrdoc-nginx

# portainer
# old
docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
# new
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

<https://docs.portainer.io/start/upgrade/docker>
<https://docs.docker.com/build/builders/>
