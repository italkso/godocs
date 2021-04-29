## SQLite



### 1. SQLite 命令和基本语法

**SQLite** 是一种C语言库，它实现了一个 [小型](https://www.sqlite.org/footprint.html)， [快速](https://www.sqlite.org/fasterthanfs.html)， [自包含](https://www.sqlite.org/selfcontained.html)， [高可靠性](https://www.sqlite.org/hirely.html)， [功能齐全](https://www.sqlite.org/fullsql.html)的 SQL数据库引擎。

最新版本的 macOS 预装了 SQLite，在命令行使用`sqlite3`命令可以验证。在出现的 SQLite 命令提示符 **sqlite>** 下，你就可以使用各种 SQLite 命令了。

#### 命令

应确保 **sqlite>** 提示符与**点命令**之间不含空格。 使用**.help**可以得到 SQLite 点命令列表。

```shell
sqlite>.help
sqlite>.show
sqlite>.quit
```

使用 **.show** 命令，来查看 SQLite 命令提示符的默认设置。

```shell
sqlite> .show
        echo: off
         eqp: off
     explain: auto
     headers: off
        mode: list
   nullvalue: ""
      output: stdout
colseparator: "|"
rowseparator: "\n"
       stats: off
       width:
    filename: :memory:
sqlite>
```

**格式化输出**设置：

```shell
sqlite>.header on
sqlite>.mode list
sqlite>.timer on
sqlite>
```

**sqlite_master** （主表）中保存数据库表的关键信息。

```shell
sqlite>.schema sqlite_master
```

上述操作产生的结果如下：

```shell
CREATE TABLE sqlite_master (
  type text,
  name text,
  tbl_name text,
  rootpage integer,
  sql text
);
```



#### 大小写和注释

**大小写**：**不区分大小写**，也有一些命令大小写敏感，如 **GLOB** 和 **glob** 在 SQLite 的语句中就有不同的含义。

**注释**：以两个连续的 "-" 字符（ASCII 0x2d）开始，并扩展至下一个换行符（ASCII 0x0a）或直到输入结束，以先到者为准。你也可以使用 C 注释，以 "`/*`" 开始，并扩展至下一个 "`*/`" 字符对或直到输入结束，以先到者为准。可跨行。

```shell
sqlite> .show -- This a comment
```



#### 数据类型

- **存储类(NULL，INTEGER，REAL，TEXT，BLOB)**

  **NULL**

  NULL 值。

  **INTEGER**

  带符号整数，根据值的大小存储在 1、2、3、4、6 或 8 字节中。布尔值被存储为整数 0（false）和 1（true）。

  **REAL**

  浮点值，存储为 8 字节的 IEEE 浮点数字。

  **TEXT**

  文本字符串，使用数据库编码（UTF-8、UTF-16BE 或 UTF-16LE）存储。

  **BLOB**

  blob 数据，完全根据它的输入存储。

- **SQLite 把日期和时间存储为 TEXT、REAL 或 INTEGER 值**

  TEXT：格式为 "YYYY-MM-DD HH:MM:SS.SSS" 的日期。
  REAL：从公元前 4714 年 11 月 24 日格林尼治时间的正午开始算起的天数。
  INTEGER：从 1970-01-01 00:00:00 UTC 算起的秒数。

- **Affinity 类型**

  TEXT、NUMERIC、INTEGER、REAL、NONE。

  

#### 运算符

运算符是一个保留字或字符，用于指定 SQLite 语句中的条件，并在语句中连接多个条件。运算符主要用于 SQLite 语句的 WHERE 子句中执行操作，如算术、比较、逻辑和位运算。WHERE 子句是用来设置 SELECT 语句的条件语句。

- 算术运算符：`+ - * /  %`

- 比较运算符：`== = != <> > >= !> < <= !<`

- 逻辑运算符：AND，NOT，OR，BETWEEN，EXISTS，IN，NOT IN，LIKE，GLOB，IS NULL，IS，IS NOT，||，UNIQUE

- 位运算符：`& | ~ << >>`等作用于位，并逐位执行操作

  

#### 表达式

表达式是一个或多个值、运算符和计算值的SQL函数的组合。

- 布尔表达式：在匹配单个值的基础上获取数据
- 数值表达式：执行查询中的任何数学运算（avg()、sum()、count()等是内置的函数）
- 日期表达式：返回当前系统日期和时间值



#### DISTINCT 关键字

DISTINCT 关键字与 SELECT 语句一起使用，作用是消除所有重复的记录，并只获取唯一一次记录。

```sqlite
SELECT DISTINCT column1, column2,.....columnN 
FROM table_name
WHERE [condition]
```



### 2. 创建、附加和分离数据库

```shell
$sqlite3 myTestDB.db
sqlite> ATTACH DATABASE 'myTestDB.db' as 'mytest';
sqlite> DETACH DATABASE 'mytest';
```

#### 创建数据库

使用 **sqlite3** 命令创建数据库，使用SQLite 的 **.databases** 命令显示数据库列表，使用 SQLite **.dump** 点命令将数据库的完整内容转储到一个 ASCII 文本文件中，也可恢复。

```shell
$sqlite3 myTestDB.db
$sqlite> .databases
sqlite>.quit
$sqlite3 myTestDB.db .dump > myTestDB.sql
$sqlite3 myTestDB.db < myTestDB.sql
```

#### 附加数据库

SQLite 使用 **ATTACH DATABASE** 语句选择一个特定的数据库，使用该命令后，所有的 SQLite 语句将在附加的数据库下执行。语法是`ATTACH DATABASE file_name AS database_name;`。

```shell
sqlite> ATTACH DATABASE 'myTestDB.db' as 'mytest';
sqlite> .database
```

myTestDB.db 是文件名，MYTEST 是数据库名。

数据库名称 **main** 是被保留用于主数据库， **temp** 则被保留用于存储临时表及其他临时数据对象。这两个数据库名称可用于每个数据库连接，且不应该被用于附加（database main / TEMP is already in use）。



#### 分离数据库

SQLite使用 **DETACH DTABASE** 语句把命名数据库从一个数据库连接分离出来，语法为 `DETACH DATABASE 'Alias-Name';`

```shell
sqlite> DETACH DATABASE 'mytest';
```

当同一个数据库文件已经被附加上多个别名，DETACH 命令将只断开给定名称的连接。

无法分离 **main** 或 **temp** 数据库。

执行分离操作后，在内存中的数据库或临时数据库会被摧毁，内容被丢弃。



### 3. 创建和删除表

使用 **CREATE TABLE** 语句创建表，使用 **.tables** 命令可以列出附加数据库中的所有表，使用 **.schema** 命令可以得到表的完整信息。如果写上 **NOT NULL** 的约束，则表示在表中创建记录时这些字段不能为 NULL。

```shell
CREATE TABLE database_name.table_name(
   column1 datatype  PRIMARY KEY(one or more columns)	NOT NULL,
   column2 datatype,
   column3 datatype,
   .....
   columnN datatype,
);
```

使用 **DROP TABLE**语句删除表，即删除表定义及其所有相关数据、索引、触发器、约束和该表的权限规范。

```shell
DROP TABLE database_name.table_name;
```



#### 4. 语句详解

SQLite 语句可以以任何关键字（如 SELECT、INSERT、UPDATE、DELETE、ALTER、DROP 等）开始，以分号（;）结束。

主要的语句如下：

- ANALYZE 语句

- AND/OR 子句

- ALTER TABLE 语句

- ALTER TABLE 语句（Rename）

- ATTACH DATABASE 语句

- BEGIN TRANSACTION 语句

- BETWEEN 子句

- COMMIT 语句

- CREATE INDEX 语句

- CREATE UNIQUE INDEX 语句

- CREATE TABLE 语句

- CREATE TRIGGER 语句

- CREATE VIEW 语句

- CREATE VIRTUAL TABLE 语句

- COMMIT TRANSACTION 语句

- COUNT 子句

- DELETE 语句

- DETACH DATABASE 语句

- DISTINCT 子句

- DROP INDEX 语句

- DROP TABLE 语句

- DROP VIEW 语句

- DROP TRIGGER 语句

- EXISTS 子句

- EXPLAIN 语句

- GLOB 子句

- GROUP BY 子句

- HAVING 子句

- INSERT INTO 语句

- IN 子句

-  Like 子句

- NOT IN 子句

- ORDER BY 子句

- PRAGMA 语句

- RELEASE SAVEPOINT 语句

- REINDEX 语句

- ROLLBACK 语句

- SAVEPOINT 语句

- SELECT 语句

- UPDATE 语句

- VACUUM 语句

- WHERE 子句

  

**Links**

[1] <https://www.sqlite.net.cn>

