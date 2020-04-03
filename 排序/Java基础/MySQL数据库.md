# MySQL数据库基本使用

所有的<>并不用写出

选自[菜鸟教程](https://www.runoob.com/mysql/mysql-tutorial.html)

#### 1.创建数据库

```mysql
create database <数据库名>
```

#### 2.删除数据库

```mysql
drop database <数据库名>
```

#### 3.选择数据库

```mysql
use <数据库名>
```

#### 4.创建表

- 如果你不想字段为 **NULL** 可以设置字段的属性为 **NOT NULL**， 在操作数据库时如果输入该字段的数据为**NULL** ，就会报错。
- AUTO_INCREMENT定义列为自增的属性，一般用于主键，数值会自动加1。
- PRIMARY KEY关键字用于定义列为主键。 您可以使用多列来定义主键，列间以逗号分隔。

- ENGINE 设置存储引擎，CHARSET 设置编码。

```mysql
mysql> CREATE TABLE runoob_tbl(
   -> runoob_id INT NOT NULL AUTO_INCREMENT,
   -> runoob_title VARCHAR(100) NOT NULL,
   -> runoob_author VARCHAR(40) NOT NULL,
   -> submission_date DATE,
   -> PRIMARY KEY ( runoob_id )
   -> )ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

#### 4.删除数据表

```mysql
drop table table_name;
```

#### 5.插入数据

```mysql
INSERT INTO table_name ( field1, field2,...fieldN )
                       VALUES
                       ( value1, value2,...valueN );
```

例子

```mysql
mysql> INSERT INTO runoob_tbl 
    -> (runoob_title, runoob_author, submission_date)
    -> VALUES
    -> ("学习 PHP", "菜鸟教程", NOW());
Query OK, 1 rows affected, 1 warnings (0.01 sec)
```

#### 6.查询数据

```mysql
SELECT column_name,column_name
FROM table_name
[WHERE Clause]
[LIMIT N][ OFFSET M]
```

- 查询语句中你可以使用一个或者多个表，表之间使用逗号(,)分割，并使用WHERE语句来设定查询条件。
- SELECT 命令可以读取一条或者多条记录。
- 你可以使用星号（*）来代替其他字段，SELECT语句会返回表的所有字段数据
- 你可以使用 WHERE 语句来包含任何条件。
- 你可以使用 LIMIT 属性来设定返回的记录数。
- 你可以通过OFFSET指定SELECT语句开始查询的数据偏移量。默认情况下偏移量为0。

#### 7.where语句

```mysql
SELECT * from runoob_tbl WHERE runoob_author='菜鸟教程';
```

在`runoob_tbl`表中搜索所有`runoob_author`为菜鸟教程的值

#### 8.update语句

```mysql
UPDATE table_name SET field1=new-value1, field2=new-value2
[WHERE Clause]
```

#### 9.delete语句

```mysql
DELETE FROM table_name [WHERE Clause]
```

#### 10.like语句

```mysql
SELECT * from runoob_tbl  WHERE runoob_author LIKE '%COM';
```

SQL LIKE 子句中使用百分号 **%**字符来表示任意字符，类似于UNIX或正则表达式中的星号 *****。

如果没有使用百分号 **%**, LIKE 子句与等号 **=** 的效果是一样的。

#### 11.UNION语句

```mysql
SELECT country FROM Websites
UNION
SELECT country FROM apps
ORDER BY country;
```

UNION会选择websites和apps里面的country列里面不同的值输出

#### 12.MYSQL排序

```mysql
SELECT * from runoob_tbl ORDER BY submission_date ASC;
```

- 你可以使用任何字段来作为排序的条件，从而返回排序后的查询结果。
- 你可以设定多个字段来排序。
- 你可以使用 ASC 或 DESC 关键字来设置查询结果是按升序或降序排列。 默认情况下，它是按升序排列。
- 你可以添加 WHERE...LIKE 子句来设置条件。

#### 13.MySQL GROUP BY 语句

GROUP BY 语句根据一个或多个列对结果集进行分组。

在分组的列上我们可以使用 COUNT, SUM, AVG,等函数。

```mysql
SELECT column_name, function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name;
```

```mysql
mysql> SELECT name, COUNT(*) FROM   employee_tbl GROUP BY name;
+--------+----------+
| name   | COUNT(*) |
+--------+----------+
| 小丽 |        1 |
| 小明 |        3 |
| 小王 |        2 |
+--------+----------+
3 rows in set (0.01 sec)
```

