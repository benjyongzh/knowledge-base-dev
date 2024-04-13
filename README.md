# dev-environment
A log to keep track of the developer tools, software and installation guides used by me.

## Environment
### WSL2 - Ubuntu 64-bit 22.04 LTS on Windows 10 Home Edition
Installation video on [YouTube](https://www.youtube.com/watch?v=1ap3hL-UR9I)
### Development Essentials
- NodeJS v21 [NodeJS Collection](https://github.com/nodesource/distributions#installation-instructions)
```
curl -fsSL https://deb.nodesource.com/setup_21.x | sudo -E bash - &&\
sudo apt-get install -y nodejs
```


- npm v8.5.1 `sudo apt install npm`
- Typescript v 5.4.1 `sudo npm i -g typescript`

- Git v2.34.1 and Github
SSH Key Integration Steps (taken from [Github's guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)):
  1. `ls -al ~/.ssh` to check for any existing keys
  2. `ssh-keygen -t ed25519 -C "<your-email-here>"` to create new ssh key (press Enter until clear)
  3. `cat ~/.ssh/id_ed25519.pub` to list out string to copy into Github for authentication
 
### zrok.io
Enables publicizing localhost URLs so anyone on the internet can reach your localhost port via tunneling. tunnel is ephemeral by default, but can be set as "reserved" to chope the zrok URL.
- Installation:
  1. Go to https://github.com/openziti/zrok/releases/tag/v0.4.26, copy the arm64.tar.gz URL
  2. On linux `/` directory, `wget <url>`
  3. `mkdir /tmp/zrok && tar -xf ./zrok*linux*.tar.gz -C /tmp/zrok`
  4. `install /tmp/zrok/zrok ~/usr/bin/`
  5. `PATH=~/usr/bin:$PATH`
  6. `zrok version`
- basic commands
```
//makes zrok invite you to create an account (required to create an account token)
zrok invite

//enable zrok account
zrok enable <account  token>

//see zrok status
zrok status

//creates "share token" of public or private resource/endpoint
zrok share <public/private> <resource/endpoint>
eg:
zrok share public http://localhost:3000

//access a private endpoint
zrok access private <share token>

//create reserved "share token" (so that it will not be ephemeral)
zrok reserve public <resource/endpoint>
//share the reserved token
zrok share reserved <resource/endpoint>
//release the reserved token (so it can never be used again)
zrok release <resource/endpoint>
```



### Bash CLI tools
`sudo apt install <tool name>`
- net-tools
  - networking for linux
- neofetch
  - get system/OS specs
- btop
  - see live info on RAM/storage/processes
- tldr
  - like a "--help", but not always applicable
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
### Jenkins Version 2.440.2
- [Install and run Jenkins as a Docker image](https://octopus.com/blog/jenkins-docker-install-guide)
  - default access:
    > http://localhost:8080/
- Build and run a new Jenkins server (as a docker container) using the code below
    - jenkins_home volume saves Jenkins server's own data (plugins etc)
    - docker.sock volume and the `which docker` volume make this Jenkins container use the host machine's docker daemon (important for creating docker images via Jenkins
```
  docker run -d -p 8080:8080 -p 50000:50000 --name jenkins-master -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):/usr/bin/docker jenkins/jenkins:lts-jdk17

```
- Jenkins plugins (on top of basic plugins upon first activation of Jenkins server)
  - Docker
    - For docker cloud. Required if the Jenkins pipeline wants to create delegate ephemeral docker agents to do the building/testing etc.
  - Docker Pipeline
  - Docker Commons
  - Blue Ocean
    - Only for better visualization of Jenkins pipeline build history
- Installation guide on [Octopus](https://octopus.com/blog/jenkins-docker-install-guide)
- Docker-in-Docker guide on [Medium](https://medium.com/@yassine.essadraoui_78000/jenkins-docker-in-docker-b7630c7b9364)
- Docker Cloud method on Jenkins
  - Gives Jenkins the ability to use ephemeral (temporary) docker containers as Jenkins agents instead of using the built-in node to do the work
```
Docker Cloud Setup steps:
1. Open Jenkins server and login
2. Create cloud based on docker
3. Cloud Details:
  - Docker Host URI `unix:///var/run/docker.sock`
  - Docker Hostname `172.17.0.1` (by default)
  - Enable docker cloud
  - Enable "Expose DOCKER_HOST"
4. Docker Agent Templates
  - Add a label and name (for eg. `docker-agent-1`)
  - Enable docker template
  - Docker Image `jenkins/ssh-agent:latest`
  - Container Settings -> Volumes From: `jenkins-master` (or whatever container name you used for the jenkins Master server)
  - Usage: `Use Node as much as possible`
  - Connect Method: `Attach Docker Container`
  - Pull Strategy: `Pull all images everytime`
```
- Jenkins Docker Slave Agent Image
  - `docker pull jenkins/agent` or `docker pull jenkins/ssh-agent`
  - Used by Docker Cloud
- Jenkins Pipeline Syntax [Doc](https://www.jenkins.io/doc/book/pipeline/)
- Groovy Syntax [Doc](https://groovy-lang.org/syntax.html#_string_interpolation)
- Docker hostname `host.docker.internal` or `172.17.0.1`
- Docker Host URI `unix: ///var/run/docker.sock` based on [Stack Overflow](https://stackoverflow.com/questions/47709208/how-to-find-docker-host-uri-to-be-used-in-jenkins-docker-plugin)

### makefile
`sudo apt install make`
- Using makefile for Docker [YouTube video](https://www.youtube.com/watch?v=44EqIY7v5xM)
