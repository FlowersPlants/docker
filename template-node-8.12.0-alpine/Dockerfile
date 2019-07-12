FROM node:8.12.0-alpine

LABEL maintainer="xinghua 764237865@qq.com"

WORKDIR /opt/local-example-web

# Bundle app source
COPY . /opt/local-example-web

# 使用npm安装依赖
RUN node -v \
  && npm -v \
  && npm install

# 使用cnpm安装依赖
# RUN npm install -g cnpm --registry=https://registry.npm.taobao.org && \
#     cnpm install

EXPOSE 80

# 直接运行js启动程序
# CMD [ "node", "index.js" ]

# 通过npm运行程序
CMD [ "npm", "start" ]
