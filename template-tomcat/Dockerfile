# 设置基础镜像
FROM tomcat

# 定义作者
LABEL maintainer="xinghua 764237865@qq.com"

# 清空原来的所有文件
RUN rm -rf /usr/local/tomcat/webapps/ROOT

# 添加项目文件
ADD . /usr/local/tomcat/webapps/ROOT

# 显示控制台
# CMD ["catalina.sh", "run"]

# 不显示控制台
# CMD [ "startup.sh" ]

# 以上两个都注释的话，则执行 tomcat 基础镜像的 CMD 命令