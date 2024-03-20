# dev-environment
A log to keep track of the developer tools, software and installation guides used by me.

## Environment
### WSL2 - Ubuntu 64-bit 22.04 LTS on Windows 10 Home Edition
[Installation video on Youtube](https://www.youtube.com/watch?v=1ap3hL-UR9I)
### Development Essentials
- NodeJS v12.22.9 and npm v8.5.1 `sudo apt install nodejs && sudo apt install npm`

[NodeJS and npm Installation Guide](https://www.hostinger.com/tutorials/how-to-install-node-ubuntu?ppc_campaign=google_search_generic_hosting_all&bidkw=defaultkeyword&lo=9062548&gad_source=1&gclid=CjwKCAjw7-SvBhB6EiwAwYdCAUvfJ0Tg9ddFReM4HACjmKJM-HASTYRalrGYdlicyvnCLcaGuA1nAxoCP8AQAvD_BwE)

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
[Download Link for VMWare](https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html.html)

[Download Link for Ubuntu image](https://ubuntu.com/download/desktop)

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
### Docker Desktop v4.28.0
- [Installation Doc for Windows](https://docs.docker.com/desktop/install/windows-install/)
- [What is Docker and how is it used](https://www.youtube.com/watch?v=Nm1tfmZDqo8)
- [How to create Docker Image](https://www.youtube.com/watch?v=EKaGsShRXNY)
### Jira
- [Youtube Guide for Integration with Github](https://www.youtube.com/watch?v=u6RsQmlX4j0)
- [How to use Jira as a Developer](https://www.youtube.com/watch?v=pLLH0dVFDvc)
