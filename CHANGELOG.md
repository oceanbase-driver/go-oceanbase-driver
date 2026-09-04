# Changelog

## v1.0.4

* 首版。基线：上游 `go-sql-driver/mysql v1.10.1`。
* 默认置上握手包 capability bit27（`OB_CLIENT_SUPPORT_ORACLE_MODE`），
  OceanBase Oracle 租户可直接用 MySQL 协议登录；否则服务端报
  `Error 1235 (0A000): Oracle tenant for current client driver is not supported`。
* 模块路径：`github.com/oceanbase-driver/go-oceanbase-driver`。
  注册到 `database/sql` 的驱动名仍为 `mysql`，不要与上游驱动混用。
* 已在 OceanBase 4.2.1.11 Oracle 租户验证：Ping、查询、预编译、事务、建表写入。
