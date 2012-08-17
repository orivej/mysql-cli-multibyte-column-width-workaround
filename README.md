MySQL command line tools display text columns as if their width is determined by the byte length of their encoding.  Consequently, multibyte encoded text gets displayed in oversized columns.  This patch provides a workarond.  It is not an ultimate solution because it guesses encoding between UTF-8 and anything else (treated as character per byte), even though it is available right away.  Proper fix seems to involve moving the offending function `cli_read_rows` from `sql-common/client.c` to `libmysql/libmysql.c`, as charset functionality is available there.

Related issue in the official bug tracker:
- https://dev.mysql.com/worklog/task/?id=2598

The patch is generated against MySQL 5.5.22.
