# 启动步骤

运行 elasticsearch 需要 vm.max_map_count 至少需要 262144 内存
切换到 root 用户修改配置 sysctl.conf
`vi /etc/sysctl.conf`
在尾行添加以下内容  
`vm.max_map_count=262144`
并执行命令
`sysctl -p`

elk 启动的时候可能会提示如下错误:
max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]

`docker-compose up` 启动
`docker-compose down` 关闭
