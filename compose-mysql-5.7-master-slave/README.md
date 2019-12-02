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

## 常见问题及解决方案

### 主从复制数据不同步

**原因：**因为在同步过程中出现主从数据不一致导致的 
**解决方法：**

1. **跳过错误数**

   ```mysql
   -- 查看主库状态，需要切换到主库
   show master status; 
   
   -- 以下操作需要切换到对应的从库
   -- 查看从库状态，
   show slave status;
   
   -- 停止从库
   stop slave; 
   
   -- 设置跳过错误书，后面的数值可以改动
   set GLOBAL SQL_SLAVE_SKIP_COUNTER=1000000000;
   
   -- 重启从库
   start slave;
   
   show slave status;
   ```

   

2. **重新设置主从日志位置**

   ```mysql
   -- master 执行获取 master_log_file 和 master_log_pos
   show master status; 
   
   -- 停止从库
   stop slave; 
   
   -- 修改从库 master_log_file 和 master_log_pos 与主库一致
   change master to master_host="129.204.194.53", master_user="root", master_password="root", master_port=3307, master_log_file="mysql-bin.000018", master_log_pos=244160466;
   
   -- 重启从库
   start slave;
   
   show slave status;
   ```

### 创建只读权限的账号

```mysql
-- 使用root用户登录到 Mysql。
-- mysql -uroot -p

-- 创建用户，并授权SELECT（可选择 select,insert,update,delete ）查询权限，授权远程访问权限，
-- 注意，命令中username/password指用户名密码，请自己指定。
-- 若要限制仅指定IP可以使用此用户访问Mysql，将%改为具IP即可。
GRANT SElECT ON *.* TO 'slave'@'%' IDENTIFIED BY "sjht123456";

-- 刷新mysql权限，使用户创建、授权生效。
flush privileges;
```



