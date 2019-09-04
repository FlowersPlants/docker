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
- 配置主数据库信息
  `change master to master_host='mysql-master-ip',master_user='slave',master_password='slave',master_log_file='mysql-bin.000001',master_log_pos=0,master_port=3306;`
- 启动 slave
  `start slave;`
- 查看状态
  `show slave status\G;`
  Slave_IO_Running: Yes
  Slave_SQL_Running: Yes
  以上两项都为 Yes，那说明没问题了。

## 读写权限设置

mysql 设置 root 超级用户只读权限[对整个库表设置只读权限]设定了后，所有的 select 查询操作都是可以正常进行的

### 设置只读

- 针对普通 MySQL 数据库用户设置为只读：
  `set global read_only=1;`
- 针对 super 类 MySQL 数据库用户设置为只读，比如 root 用户
  `set global super_read_only=1;`
- 设定全局锁,如果只是需要只读，并不需要加锁
  `flush tables with read lock;`
- 查询全局变量表数据情况
  `show global variables like "%read_only%";`

### 设置读写

- 针对普通 MySQL 数据库用户设置为读写
  `set global read_only=0;`
- 针对 super 类 MySQL 数据库用户设置为读写，比如 root 用户
  `set global super_read_only=0;`
- 解锁
  `unlock tables;`
