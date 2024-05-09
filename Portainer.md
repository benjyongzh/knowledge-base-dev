v2.19
# Introduction
Allows for easier management of #containers and #images with a GUI.
# Installation
Guide from Portainer docs [here](https://docs.portainer.io/start/install-ce/server/docker/wsl).
## Installing Portainer as a docker container
1. Create #docker volume for Portainer
```
docker volume create portainer_data
```
2. Install Portainer image and container while using localhost's docker socket
```
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```
3. Access Portainer on port 9443 `https://localhost:9443`
# How To Use