# eplain
## 链接: https://www.cnblogs.com/tufujie/p/9413852.html
## type
NULL
system、const
eq_ref
ref
range
index
all

mysql 为什么不建议为NULL
https://www.cnblogs.com/balfish/p/7905100.html

mysql 为什么建议主键连续

## mysql各种日志

### binlog: 二进制日志
### undo log: 回滚日志
作用: 保证数据的原子性，记录事务发生之前的一个版本，用于回滚，innodb事务可重复读和读取已提交 隔离级别就是通过mvcc+undo实现

### redo 重做日志
作用: 确保日志的持久性，防止在发生故障，脏页未写入磁盘。重启数据库会进行redo log执行重做，达到事务一致性

### relay log
作用: 用于数据库主从同步，将主库发来的bin log保存在本地，然后从库进行回放