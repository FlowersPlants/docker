# Elasticsearch-5.6.14

安装后可能出现以下问题

- 打开 elasticsearch-head 跨域
  进入容器修改 `config/elasticsearch.yml` ,添加以下配置：

  ```yaml
  http.cors.enabled: true
  http.cors.allow-origin: '*'
  ```

  然后重启该容器

- 登录问题
  Elasticsearch-5.6.14 使用 Xpack 插件做安全验证，默认许可证有效期 30 天，为了方便把 xpack 禁用即可。在环境变量中加入：
  `- 'xpack.security.enabled=false'`
