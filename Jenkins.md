Version 2.440.2
# Introduction
#jenkins is a #CICD server that allows developers to create automated pipelines to quicken the #SLDC. It can be used in conjunction with many other tools and technologies, such as #docker and [[Google Cloud]].
# Installation
- [Install and run Jenkins as a Docker image](https://octopus.com/blog/jenkins-docker-install-guide)
	- default access: "http://localhost:8080/"
- Installation guide on [Octopus](https://octopus.com/blog/jenkins-docker-install-guide)
# How To Use
## Build and run a new Jenkins server (as a docker container)
Guide: Docker-in-Docker guide on [Medium](https://medium.com/@yassine.essadraoui_78000/jenkins-docker-in-docker-b7630c7b9364)

Run this script in host machine:
```
  docker run -d -p 8080:8080 -p 50000:50000 --name jenkins-master -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):/usr/bin/docker jenkins/jenkins:lts-jdk17
```
### What the script means:
- `jenkins_home` volume saves Jenkins server's own data (plugins etc)
- `docker.sock` volume and the `which docker` volume make this Jenkins container use the host machine's [[Docker Daemon]] (important for creating docker images via Jenkins)
## Jenkins plugins (on top of basic plugins upon first activation of Jenkins server)
- Docker
	- For #docker cloud. Required if the Jenkins pipeline wants to create delegate #ephemeral docker agents to do the building/testing etc.
- Docker Pipeline
- Docker Commons
- Blue Ocean
    - Only for better visualization of Jenkins pipeline build history
## Docker Cloud method on Jenkins
Gives Jenkins the ability to use ephemeral (temporary) docker containers as Jenkins agents instead of using the built-in node to do the work.
### Docker Cloud Setup steps:
1. Open Jenkins server and login
2. Create cloud based on docker
3. Cloud Details:
	1. Docker Host URI `unix:///var/run/docker.sock
	2. Docker Hostname `172.17.0.1` (by default)
	3. Enable docker cloud
	4. Enable "Expose DOCKER_HOST"
	5. Test Connection.
	    - If no permission, check permissions of /var/run/docker.sock with:
          `ls -l /var/run/docker.sock`
		- If output is srw-rw----, use command below to change it to srw-rw-rw-:
          `sudo chmod 666 /var/run/docker.sock`
        - Test Connection again.
4. Docker Agent Templates
	  - Add a label and name (for eg. `docker-agent-1`)
	  - Enable docker template
	  - Docker Image `jenkins/ssh-agent:latest`
	  - Remote File System Root: `home/jenkins`
	  - Container Settings -> Volumes From: `jenkins-master` (or whatever container name you used for the jenkins Master server)
	  - Usage: `Use Node as much as possible`
	  - Connect Method: `Attach Docker Container`
	  - Pull Strategy: `Pull all images everytime`
## Jenkins Docker Slave Agent Image
Install with: `docker pull jenkins/agent` or `docker pull jenkins/ssh-agent`
- Used by Docker Cloud
- Jenkins Pipeline Syntax [Doc](https://www.jenkins.io/doc/book/pipeline/)
- Groovy Syntax [Doc](https://groovy-lang.org/syntax.html#_string_interpolation)
- Docker hostname `host.docker.internal` or `172.17.0.1`
- Docker Host URI `unix: ///var/run/docker.sock` based on [Stack Overflow](https://stackoverflow.com/questions/47709208/how-to-find-docker-host-uri-to-be-used-in-jenkins-docker-plugin)
## Linking [[Google Cloud]] to Jenkins
[Youtube Video Instructions](https://www.youtube.com/watch?v=eHtRGc6EMY4&ab_channel=CloudBeesTV)
### Prerequisites:
JenkinsMaster docker container must have an ENV variable of "GOOGLE_APPLICATION_CREDENTIALS" set to a location of secret manager key (for eg /var/cache/jenkins/gcp-jenkins-project.json)
### Linking Steps
  1. Install GCP secrets manager plugin on Jenkins
  2. Set GCP projectname to projectID of gcloud project
  3. Create service account in gcloud just for jenkins, and give secrets accessor + secrets viewer roles to this new account
  4. Create private key for service account and save text to /var/cache/jenkins/gcp-jenkins-project.json of Jenkins docker container
  5. Make sure Jenkins docker container as ENV GOOGLE_APPLICATION_CREDENTIALS point to location of json for private key from step 4
  6. Restart Jenkins container
  7. Create new secret in Google Secrets Manager, with label of:
    jenkins-credentials-type: [string/file/username-password/ssh-user-private-key/certificate] (pick only one out of these 5)
  8. In secret will appear in Jenkins credentials automatically (Jenkins will get gcloud info every 5mins based on observations)
  9. In Jenkins pipeline, point an env variable to the new secret by using:
```
	environment {
		MY_ENV_BLABLA = credentials('name-of-my-secret-bla-bla')
	}
```
