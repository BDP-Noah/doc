# 使用ODBC连接数据库

## 安装对应的驱动

驱动安装请参照[数据库驱动](/数据库驱动)

## 连接参数说明

![](http://noah.bj.bcebos.com/doc/img/2df07d2aec00ddc9e53aa9c1983dea74.png)

### ODBC名称
所创建的ODBC数据源的名称

!> 目前仅支持32位的ODBC连接, 在64位windows系统中, 系统默认的ODBC管理程序是64位的, 32位的管理程序为:`C:\Windows\SysWOW64\odbcad32.exe`

### 用户名
该数据库的用户名

### 密码
该数据库的密码

### 额外参数
大多数ODBC数据库的层次结构为: Catalog/Schema/Table三层结构, 因为数据库本身的限制或者使用习惯的原因, 各种数据库对这种结构的使用方式不同:

* `Catalog模式`: 有的数据库使用单Catalog对应多Schema的形式(例如MySQL); 这种情况下, Catalog是固定的, 然而有多个Schema;
这时配置为Schema模式, 并指定Catalog名称, 同步客户端会自动获取该Catalog下所有的Schema, 简化配置流程.


* `Schema模式`: 反之, 部分数据库使用单个Schema对应多个Catalog的形式(例如SQL Server); 此时会自动获取符合该Schema的所有Catalog.

!> Sybase ASE不支持Schema模式


### 分隔标识符
在执行SQL查询时, 数据库名, 表名, 字段名需要正确的分隔方式, 以防止某些特殊的符号造成数据同步异常.

例如在Oracle中, 假设表`STUDENT`中有个字段名为`First Name`(包含空格), 执行以下SQL会造成语法错误:

```SQL
SELECT STUDENT.First Name from STUDENT
```
此时若增加合适的字段分隔标识符即可避免:
```SQL
SELECT "STUDENT"."First Name" from "STUDENT"
```
其中双引号`""`就是Oracle的字段引用. 注意`字段引用`配置项包含两个字符, 分别表示开始和结束(如SQL Server的为`[]`). 每种数据库的分隔标识符不同, 文档末尾总结了一些常用的数据库类型, 未涵盖的请查阅数据库官方文档.

### 字段设置

> 字段设置比较复杂, 一般情况下保持默认即可

结构示例:

```json
{
  "*": {
    "where": "",
    "select": ""
  },
  "datetime": {
    "where": null,
    "select": "to_char([{tb_name}].[{fd_name}])"
  }
}
```
结构为`[字段类型].[字段位置] = [字段处理函数]`, 其中提供了两个变量供使用:

1. `{tb_name}`: 表名称
2. `{fd_name}`: 字段名称

例如上例中`datetime.select = to_char([{tb_name}].[{fd_name}])`, 可以翻译为当字段类型为`datetime`且这个字段出现在`SELECT`子句中时, 使用`to_char([{tb_name}].[{fd_name}])`来构造改字段的使用.

其中[字段类型]中的`*`为通配符, 表示对所有的字段类型生效

#### 示例1: 将PostgresQL中的date类型转换为标准年月日时分秒格式

表`User`:

|字段名|字段类型|示例数据|
|---|---|---|
|id|int|1|
|birth|date|1921-09-09|

如果不做任何设置, 执行的SQL将会是
```SQL
SELECT "User"."id", "User"."birth" FROM "USER"
```

结果为:

|id|birth|
|---|---|
|1|1921-09-09|

这种格式的日期BDP是无法计算的, 因此增加字段设置即可解决此问题:

```python
{
  "date": {
    "select": "TO_CHAR("{tb_name}"."{fd_name}", 'YYYY-MM-DD HH24:MI:SS')"
  }
}
```

SQL将会被解析为:
```SQL
SELECT "User"."id", TO_CHAR("User"."birth", 'YYYY-MM-DD HH24:MI:SS') FROM "USER"
```

而结果为:

|id|birth|
|---|---|
|1| 1921-09-09 00:00:00 |

#### 示例2: 对Hive中的timestamp字段转换为标准年月日时分秒格式


### 常用数据库参数配置

|数据库名称|额外参数(模式)|额外参数值|引用设置|
|---|---|---|---|
|MySQL|Catalog||**``** ([反单引号](https://baike.baidu.com/item/%60/5633084?fr=aladdin))
|SQL Server|Schema|dbo|**[]** (英文中括号)
|Sybase|Schema|dbo|**[]** (英文中括号)
|Oracle|Catalog|sid|**""** (英文双引号)
