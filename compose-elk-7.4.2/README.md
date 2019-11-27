# ELK 环境搭建

## 启用认证

- 进入容器执行 `/usr/share/elasticsearch/bin/elasticsearch-setup-passwords interactive` 初始化密码
- 取消配置文件的 `user` 和 `password` 注释
- 依次重启容器
