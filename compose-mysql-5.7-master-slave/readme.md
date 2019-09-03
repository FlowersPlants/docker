# 执行步骤

## 使用步骤

进入当前目录执行 `docker-compose up -d`，即可创建 1 主 2 从的 mysql 主从复制集群

### 主数据库配置

- 登录 mysql
  `mysql -u root -p;`

- 创建一个用户用于同步
  `create user 'slave'@'172.17.0.%' identified by 'slave';`

- 给用户赋值权限
  `grant replication slave on *.* to 'slave'@'172.17.0.%' identified by 'slave';`

- 使配置生效
  `flush privileges;`

- 重启数据库服务

## 从数据库配置

- 登录 mysql
  `mysql -u root -p;`

- 停止 slave
  `stop slave;`

- 配置
  `change master to master_host='mysql-master-ip',master_user='slave',master_password='slave',master_log_file='mysql-bin.000001',master_log_pos=0,master_port=3306;`

- 启动
  `start slave;`

- 查看状态
  `show slave status\G;`
  Slave_IO_Running: Yes
  Slave_SQL_Running: Yes
  以上两项都为 Yes，那说明没问题了。
