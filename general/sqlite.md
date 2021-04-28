## SQLite

**SQLite** 是一种C语言库，它实现了一个 [小型](https://www.sqlite.org/footprint.html)， [快速](https://www.sqlite.org/fasterthanfs.html)， [自包含](https://www.sqlite.org/selfcontained.html)， [高可靠性](https://www.sqlite.org/hirely.html)， [功能齐全](https://www.sqlite.org/fullsql.html)的 SQL数据库引擎。

最新版本的 macOS 预装了 SQLite，在命令行使用`sqlite3`命令可以验证。在出现的 SQLite 命令提示符 **sqlite>** 下，你就可以使用各种 SQLite 命令了。

### 1. SQLite 命令

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



### 2. SQLite 基本语法

SQLite **不区分大小写**，但也有一些命令是大小写敏感的，比如 **GLOB** 和 **glob** 在 SQLite 的语句中有不同的含义。

SQL **注释**以两个连续的 "-" 字符（ASCII 0x2d）开始，并扩展至下一个换行符（ASCII 0x0a）或直到输入结束，以先到者为准。你也可以使用 C 注释，以 "`/*`" 开始，并扩展至下一个 "`*/`" 字符对或直到输入结束，以先到者为准。可跨行。

```shell
sqlite> .show -- This a comment
```

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



### 3. 创建数据库

```shell
$sqlite3 myTestDB.db
$sqlite> .databases
sqlite>.quit
$sqlite3 myTestDB.db .dump > myTestDB.sql
$sqlite3 myTestDB.db < myTestDB.sql
```

- 使用 **sqlite3** 命令创建数据库
- 使用SQLite 的 **.databases** 命令显示数据库列表
- 使用 SQLite **.dump** 点命令将数据库的完整内容转储到一个 ASCII 文本文件中，也可恢复。





**Links**

[1] <https://www.sqlite.net.cn>

