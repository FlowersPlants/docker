FROM jenkins:2.60.3
USER root
ARG dockerGid=999

RUN echo "docker:x:${dockerGid}:jenkins" >> /etc/group

#USER jenkins