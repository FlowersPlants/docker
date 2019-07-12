# 设置基础镜像 
FROM nginx:1.15

# 定义作者
LABEL maintainer="xinghua 764237865@qq.com"

# 删除nginx 默认配置
RUN rm /etc/nginx/conf.d/default.conf

# 添加default.conf
ADD ./nginx/default.conf /etc/nginx/conf.d/

# 将dist文件中的内容复制到 /usr/share/nginx/html/ 这个目录下面
COPY static/ /usr/share/nginx/html/static/
COPY index.html  /usr/share/nginx/html/