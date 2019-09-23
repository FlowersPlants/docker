# 使用说明

默认情况下，您可以 admin 使用密码登录 admin。

## 要求

由于 SonarQube 使用嵌入式 Elasticsearch，因此请确保 Docker 主机配置符合 Elasticsearch 生产模式要求和 File Descriptors 配置。

例如，在 Linux 上，可以通过在主机上以 root 用户身份运行以下命令来设置当前会话的建议值：

```linux
sysctl -w vm.max_map_count=262144
sysctl -w fs.file-max=65536
ulimit -n 65536
ulimit -u 4096
```

## 汉化

- 使用 admin 登录 sonarqube
- Administration >Marketplace
- 在搜索框中输入 chinese，出现一个 Chinese Pack，点击右侧的 install 按钮。
- 安装成功后，会提示重启 SonarQube 服务器。
