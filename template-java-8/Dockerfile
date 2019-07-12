FROM java:8

LABEL maintainer="xinghua<764237865@qq.com>"
WORKDIR /opt/example/

ADD ./lib /opt/example/lib
ADD ./resources /opt/example/resources
ADD ./local-example*.jar /opt/example/app.jar

EXPOSE 8800
# EXPOSE 20800

ENTRYPOINT [ "java","-jar","example.jar" ]