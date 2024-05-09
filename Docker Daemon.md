Engine v26.0.0, API v1.45
# Introduction
The real engine for running #docker containers from images. As a standalone, it can only be used as a #CLI tool without a GUI. For #docker with a #GUI, refer to [[Docker Desktop]].
# Installation
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
- [Installation Doc](https://docs.docker.com/engine/install/ubuntu/) for Ubuntu 64-bit
# How To Use
## Basic Docker Commands
```
//show running containers
docker ps

//show all containers
docker ps -a

//show all images
docker images 

//build an image based on Dockerfile
docker build -t <image-tag> -f <location-of-Dockerfile>

//run an image as a new docker container
docker run -d -p <localhost-port>:<image-port-exposed> --name <container-name> <image-tag/image-ID-to-create-container-out-of>

//control start/stop of a container
docker start <container-name/ID>
docker stop <container-name/ID>

//info
docker version
docker info
docker inspect <network or container or image>
```
