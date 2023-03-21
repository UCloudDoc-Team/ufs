

# 产品限制

### 单账户配额
单个账户可创建的文件系统实例个数限制为 100 个。

### 文件系统限制
  * 文件系统支持 TCP 方式的 NFSv4.0, NFSv3, SMB协议
  * 目前容量型最大购买容量为 100TB，性能型最大购买容量为 20TB，如需更大空间请联系技术支持
  * 单文件最大 size 限制为 1TB
  * 单文件系统 inode 数目限制为 100000000
  * 单台云主机内可挂载的文件系统实例个数不限制
  * 单个文件系统允许挂载的主机个数不限制
  * 单个文件系统的挂载点个数限制为 5 个，注意挂载点个数限制并不是可挂载文件系统的主机个数限制，只要在挂载点允许的 VPC 内的主机都可以访问指定文件系统
  * 容量型单文件系统吞吐随容量增长，单 TB 吞吐为 120MBps，上限为 20GBps
  * 性能型单文件系统公测期吞吐上限为 1GBps，如需更高吞吐请联系技术支持
  * 文件系统目前仅支持扩容操作，不支持缩容操作
  * NFSv4 协议的文件系统支持基于 VPC 实现的跨账号、跨地域访问

### 协议限制
|协议类型      |不支持的协议和语义 |
|------------ |------------ |
|NFSv4.0	   |不支持的 Attributes 包括:ACL、WINDOWS\_FILE\_ATTRIBUTES(HIDDEN、ARCHIVE、SYSTEM)、MIMETYPE、QUOTA\_AVAIL\_HARD、 QUOTA\_AVAIL\_SOFT、QUOTA\_USED、TIME\_BACKUP、TIME\_CREATE；不支持 OP 包括：DELEGPURGE、DELEGRETURN、LOOKUPP、OPENATTR；不支持 Delegation|
|NFSv3	   |不支持ACL和LOCK|
|SMB	     |暂不支持创建大小写同名的文件、目录|

### 计费策略
不支持按需使用，目前您只能通过预先购买容量的方式来使用文件存储。
