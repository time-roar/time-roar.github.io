# MySql

## BinLog

是否启用binlog日志
```sql
show variables like 'log_bin';
```

查看详细的日志配置信息
```sql
show global variables like '%log%';
```

数据存储目录
```sql
show variables like '%dir%';
```

查看binlog的目录
```sql
show global variables like "%log_bin%";
```

查看当前服务器使用的biglog文件及大小
```sql
show binary logs;
```

事件查询命令

```sql
-- IN 'log_name' ：指定要查询的binlog文件名(不指定就是第一个binlog文件)
-- FROM pos ：指定从哪个pos起始点开始查起(不指定就是从整个文件首个pos点开始算)
-- LIMIT [offset,] ：偏移量(不指定就是0)
-- row_count ：查询总条数(不指定就是所有行)
show binlog events [IN 'log_name'] [FROM pos] [LIMIT [offset,] row_count];
```

查看 binlog 内容
```sql
show binlog events;
```

查看具体一个binlog文件的内容 （in 后面为binlog的文件名）
```sql
show binlog events in 'binlog.000038';
```

设置binlog文件保存事件，过期删除，单位天
```sql
set global expire_log_days=7; 
```

删除当前的binlog文件
```sql
reset binlog; 
```

删除指定日期前的日志索引中binlog日志文件
```sql
purge master logs before '2021-12-31 14:00:00';
```

删除指定日志文件
```sql
purge master logs to 'binlog.000038';
```

