# 数据库常见问题
## mysql不支持group by的解决方法

下载安装的是最新版的mysql5.7.x版本，默认是开启了 `only_full_group_by` 模式的，但开启这个模式后，原先的` group by `语句就报错，然后又把它移除了。

一旦开启 `only_full_group_by `，感觉，`group by` 将变成和 `distinct `一样，只能获取受到其影响的字段信息，无法和其他未受其影响的字段共存，这样，`group by` 的功能将变得十分狭窄了

`only_full_group_by` 模式开启比较好。因为在 mysql 中有一个函数： any_value(field) 允许，非分组字段的出现（和关闭 only_full_group_by 模式有相同效果）。

具体出错提示：

> [Err] 1055 - Expression #1 of ORDER BY clause is not in GROUP BY clause and contains nonaggregated column 'information_schema.PROFILING.SEQ' which is not functionally dependent on columns in GROUP BY clause; this is incompatible with sql_mode=only_full_group_by

解决方案如下:

- 查看sql_mode

  ```sql
  select @@global.sql_mode;
  ```

- 结果为

  > ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION

- 去掉ONLY_FULL_GROUP_BY，重新设置值。

  ```sql
  select @@global.sql_mode;
  set sql_mode='STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION';
  set global sql_mode='STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION';
  set session sql_mode='STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION';
  ```

- 上述数据库重启会失效,如果想持久化生效,请修改文件`my.cnf`

  ```properties
  [mysqld]
  sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION
  ```

  
