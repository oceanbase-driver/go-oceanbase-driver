# go-oceanbase-driver

Go 的 OceanBase 驱动，基于 `go-sql-driver/mysql v1.10.1`，用法与标准 MySQL 驱动完全一致，
区别是默认置上握手包 capability bit27，可直连 OceanBase **Oracle 租户**。
未打补丁的 MySQL 协议驱动连 Oracle 租户会被服务端拒绝：

```text
Error 1235 (0A000): Oracle tenant for current client driver is not supported
```

原理：OceanBase 登录时检查该位（`OB_CLIENT_SUPPORT_ORACLE_MODE`，
与 MySQL 8.0 的 `CLIENT_QUERY_ATTRIBUTES` 同一位），mysql 8.0 客户端默认置位，
Go 驱动默认没置。本驱动默认置上，对 MySQL / MariaDB / OB MySQL 租户无副作用。

## 安装

```shell
go get github.com/oceanbase-driver/go-oceanbase-driver@v1.0.4
```

注意：不要在同一个程序里同时引用上游 `go-sql-driver/mysql` 和本驱动，
两者注册的驱动名都是 `mysql`，会 panic。

## 用法

```go
import (
	"database/sql"

	_ "github.com/oceanbase-driver/go-oceanbase-driver"
)

db, err := sql.Open("mysql", "user@tenant#cluster:password@tcp(host:9090)/dbname?timeout=10s")
// 之后就是标准 database/sql 用法
```

Oracle 租户示例：

```go
var user string
err := db.QueryRow("SELECT USER FROM DUAL").Scan(&user)
```

## 注意事项

1. 业务 SQL 须用 Oracle 方言（如 `FROM DUAL`、`SYSDATE`），不支持反引号和 `LIMIT`。
2. `LastInsertId` 不支持（Oracle 无自增列），请用序列；`RowsAffected` 正常。
3. DSN 写法等细节见上游文档：https://github.com/go-sql-driver/mysql

## 版本

版本号与验证过的上游版本对齐发布。v1.0.4 = 上游 v1.10.1 + Oracle 租户登录补丁，
已在 OceanBase 4.2.1.11 Oracle 租户验证：Ping、查询、预编译、事务、建表写入。

## 协议

MPL-2.0，与上游一致。原作者见 AUTHORS。
