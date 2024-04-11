# dev-environment
A log to keep track of the developer tools, software and installation guides used by me.

## Environment
### WSL2 - Ubuntu 64-bit 22.04 LTS on Windows 10 Home Edition
Installation video on [YouTube](https://www.youtube.com/watch?v=1ap3hL-UR9I)
### Development Essentials
- NodeJS v21 [NodeJS Collection](https://github.com/nodesource/distributions#installation-instructions) ```curl -fsSL https://deb.nodesource.com/setup_21.x | sudo -E bash - &&\
sudo apt-get install -y nodejs```


- npm v8.5.1 `sudo apt install npm`
- Typescript v 5.4.1 `sudo npm i -g typescript`

- Git v2.34.1 and Github
SSH Key Integration Steps (taken from [Github's guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)):
1. `ls -al ~/.ssh` to check for any existing keys
2. `ssh-keygen -t ed25519 -C "<your-email-here>"` to create new ssh key (press Enter until clear)
3. `cat ~/.ssh/id_ed25519.pub` to list out string to copy into Github for authentication


### Bash CLI tools
`sudo apt install <tool name>`
- net-tools
- neofetch
- btop
- tldr
### VMWare Workstation 17 Player - Ubuntu 64-bit 22.04 LTS
[Download Link](https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html.html) for VMWare

[Download Link](https://ubuntu.com/download/desktop) for Ubuntu image

## IDE
### Visual Studio Code
Used for all coding except Java.

VSCode Extensions:
- Arrow Function Snippets
- Atom One Dark Theme
- ES7+ React/Redux/React-Native snippets
- JavaScript (ES6) code snippets
- Typescript React code snippets
- Vue 3 Snippets
- Vue VSCode Snippets
- WSL
- ESLint
- Live Server
- Prettier - Code formatter
- Prettier ESLint
- Tailwind Config Viewer
- Tailwind CSS IntelliSense
- Todo Tree
- Vue - Official

### IntelliJ IDEA Community Edition
Used for Java.

## Software
### Docker Desktop v4.28.0 (Unable to use Docker Cloud plugin in Jenkins. Use Docker Engine instead)
- [Installation Doc](https://docs.docker.com/desktop/install/windows-install/) for Windows
- What is Docker and how is it used [YouTube video 1](https://www.youtube.com/watch?v=Nm1tfmZDqo8), [YouTube video 2](https://www.youtube.com/watch?v=pg19Z8LL06w&list=PLoRikNuYMkcBolm6Tfmj3L3-YmkDMzP89&index=9)
- [Docker cheatsheet/docs](https://www.squash.io/docker-how-to-workdir-run-cmd-env-variables/#:~:text=The%20WORKDIR%20command%20in%20Docker,Docker%20container%20is%20set%20to%20%2F%20.)
- How to create Docker Image [YouTube video](https://www.youtube.com/watch?v=EKaGsShRXNY)
- Docker compose Introduction [YouTube video](https://www.youtube.com/watch?v=SXwC9fSwct8&list=PLoRikNuYMkcBolm6Tfmj3L3-YmkDMzP89&index=10)
- [env files, buildtime vs runtime for Docker and NextJS](https://www.saltycrane.com/blog/2021/04/buildtime-vs-runtime-environment-variables-nextjs-docker/#setting-dynamic-buildtime-environment-variables-that-are-available-at-runtime-also)

### Docker Daemon (Engine v26.0.0, API v1.45)
Installation:
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
- Docker hostname `host.docker.internal`
- Docker Host URI `unix: ///var/run/docker.sock` based on [Stack Overflow](https://stackoverflow.com/questions/47709208/how-to-find-docker-host-uri-to-be-used-in-jenkins-docker-plugin)
- Basic docker commands:
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

### Jira
- Guide for Integration with Github [Youtube video](https://www.youtube.com/watch?v=u6RsQmlX4j0)
- How to use Jira as a Developer [YouTube video](https://www.youtube.com/watch?v=pLLH0dVFDvc)
### Jenkins
- [Install and run Jenkins as a Docker image](https://octopus.com/blog/jenkins-docker-install-guide)
- Jenkins Master on Docker
  - `docker run -d -p 8080:8080 -p 50000:50000 --name jenkins-master -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):/usr/bin/docker jenkins/jenkins:lts-jdk17`
  - Installation guide on [Octopus](https://octopus.com/blog/jenkins-docker-install-guide)
  - Docker-in-Docker guide on [Medium](https://medium.com/@yassine.essadraoui_78000/jenkins-docker-in-docker-b7630c7b9364)
  - Plugins
    - Docker
    - Docker Pipeline
    - Docker Commons 
- Jenkins Docker Slave Agent
  - `docker pull jenkins/agent` or `docker pull jenkins/ssh-agent`
  - Docker-in-Docker guide on [Medium](https://medium.com/@yassine.essadraoui_78000/jenkins-docker-in-docker-b7630c7b9364)
- Jenkins Pipeline Syntax [Doc](https://www.jenkins.io/doc/book/pipeline/)
- Groovy Syntax [Doc](https://groovy-lang.org/syntax.html#_string_interpolation)

### makefile
`sudo apt install make`
- Using makefile for Docker [YouTube video](https://www.youtube.com/watch?v=44EqIY7v5xM)
