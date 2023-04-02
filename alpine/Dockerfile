FROM jenkins/jenkins:alpine

USER root
RUN groupadd -g 281 docker
RUN usermod -aG docker jenkins

RUN apk add --no-cache docker docker-compose

USER jenkins
RUN jenkins-plugin-cli --plugins "blueocean docker-workflow"
