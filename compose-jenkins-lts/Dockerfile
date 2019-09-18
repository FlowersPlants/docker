FROM jenkins/jenkins:lts
USER root
ARG dockerGid=999

RUN echo "docker:x:${dockerGid}:jenkins" >> /etc/group

#USER jenkins