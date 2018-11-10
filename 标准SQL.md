
[TOC]
# 零、创建数据库、表的结构
```
CREATE DATABASE database_name; # 创建数据库
DROP database_name; # 删除数据库
```

## 第 17 章 创建、更新、删除、重命名表的结构(table)
- 创建表

```sql
CREATE TABLE table_name
(      col1 该列数据类型 NOT NULL / NULL ,
       col2 该列数据类型 NOT NULL / NULL,
       col3 该列数据类型 ，
       col3 该列数据类型 NOT NULL DEFUALT 10
);
```
- 更新表

增加字段、删除字段
尽可能减少对表结构的修改，在设计数据库的时候，尽可能更改表考虑

```SQL
ALTER TABLE table_name
ADD col_name 该列数据类型；
ALTER TABLE table_name
DROP COLUMN col_name;
```

- 更加复杂的表结构更新

1. 创建一个新结构的表
2. 使用`INSERT SELECT`语句将旧表移动到新表
3. 检验新表中的数据
4. 旧表删除，如果需要的话
5. 重命名新表
6. 根据需求，添加SQL的高级特性

- 删除表

```sql
DROP TABLE table_name;
```

- 重命名表 **此处有待根据使用的数据系统确定**

```sql
RENAME old_table_name new_table_table
```

- - -

# 一、增

## 第 15 章 插入数据

- 将数据以行的形式插入至数据表中
  `INSERT` 插入一行
  `INSERT SELECT`插入多行

1. 插入完整的行

```sql
  # 这种写法，插入的数据依赖于表定义的结构，数据由`VALUES`给出，不是很安全，避免使用
  INSERT INTO table_name
  VALUES(col1_data,
         col2_data,
         col3_data,
         col4_data,
         NULL);
```

```sql
  # 更安全，但是繁琐的方法,tables表 中明确提供了列名，VALUES 必须按照指定顺序匹配列名
  INSERT INTO table_name(col1,
                         col2,
                         col3,
                         col4,
                         col5)
  VALUES(col1_data,
         col2_data,
         col3_data,
         col4_data,
         NULL);
```

2. 插入行的某一部分，也就是其中的某些字段

```sql
# 插入部分行，省略其中的某些字段，该字段必须满足允许`NULL`值或给出默认值
  INSERT INTO table_name(col1,
                         col2,
                         col3 NULL,
                         col4,
                         col5 DEFUALT 10)
  VALUES(col1_data,
         col2_data,

         col4_data,
         NULL);
```

3. 插入查询语句的结果

```SQL
# 这里要建立新表，并且`SELECT`语句返回的是列的位置，第一列填充制定的第一列
INSERT INTO table2(col1,
                   col2,
                   col3,
                   col4)
SELECT col5,
       col6,
       col7,
       col8
From table1;
```

- 从一个表复制到另一个表

  使用`SELECT INTO`

```sql
SELECT *
INTO table2
FROM table1;
```
- - -
# 二、删 & 改

## 第 16 章 更新和删除数据(行 & 列)

- 更新表中特定的行
- 更新表中所有的行

要更新的表，总是以要更新的表名开始
列名和他们的新值,以`SET`子句进行设置,新值可以使用子查询
确定要更新行的conditions,以`WHERE`子句结束

```sql
UPDATE table_name
SET col1 = new_value1,
    col2 = new_value2,
    ...
    coln = new_value3
WHERE  another = conditions;
```

- 删除某行中某列的值

```
# 设置为`NULL`
UPDATE table_name
SET col1 = new_value1,
    col2 = NULL,
    ...
    coln = new_value3
WHERE  another = conditions;
```

- 删除表中特定的整行
- 删除表中所有的行
- 均指删除表中的内容，而不是表的结构

```sql
DELETE FROM table_name
WHERE col = conditions;
```
以上更新、删除语句均携带了`WHERE`子句，
若无，则更新或者删除表中的所有行
每个表中都有主键，在`WHERE`中尽量使用他
在进行更新或者删除操作前，先用`SELECT`测试过滤`conditons`

- - -
# 三、查

## 第 1 章

数据库是是通关数据库管理系统创建和操纵的容器
表（table）是数据库中结构化的文件，每张表都有唯一的名字来标识自己，
表是由一列或者多列组成的
表中的数据按照行进行存储的
将能够区别其他行的列成为主键，其定义见《SQL 必知必会》P6

```SQL
SELECT[返回的列或者表达式]
FROM[要求检索的表]
WHERE[行级过滤]
GROUP BY[无序分组]
HAVING[组级过滤]
ORDER BY[有序分组]
LIMIT n1 OFFSET n2[限制从 n2 行起返回 n1 行]
#每条 SQL 语句以 `;`结束
```

内联结 自联结 自然联结 交叉联结 左 右 全外联结

## 第 2 章 检索数据（SELECT）

关键字：sql 中的保留字，不能作为列或者表的名字
sql 语句不区分大小写，sql 关键字一般大写，表名和列名一般小写
数据库系统在处理 sql 语句时，其中空格均被忽略，格式只是为了便于阅读
多条 sql 语句，必须使用`;`为结尾区分

使用`SELECT`检索数据，必须给出
想选择什么
从什么地方选
返回表中的所有行，并且返回的数据没有特定的顺序

```SQL
# 检索单列
SELECT col1 #目标列名
FROM table_name;#从哪儿
```

```SQL
# 检索多列
SELECT col1,col2,...,coln
FROM table_name;
```

除非确实需要使用所有列，否则别使用`*`，但是这会降低性能
```
# 检索所有列
SELECT *
FROM table_name;
```

使用`DISTINCT`检索不同的值，过滤重复的值，必须将其放在列名前面，但是作用于紧随其后的所有列，重复的值只按照一次计算

```SQL
# 检索不同的值
SELECT DISTINCT cols
FROM table_name;
```

限制返回一定数量的行数，不同的DBMS不同，这里特指MySql、Postgresql、SQLite
`LIMIT n` 指定返回的数目 n 
`OFFSET n` 指定从第 n 行开始计数，默认从第 0 行开始

```SQL
# 返回前五行的数据
SELECT col1
FROM table_name;
LIMIT 5;

# 返回从第 5 行开始的 5 条记录
SELECT col1
FROM table_name;
LIMIT 5 OFFSET 5;
```

使用注释
1. 使用`--`进行行内注释
2. 使用`#`进行行内注释
3. 使用`/* XXXXXXXX */` 进行多行注释

## 第 3 章 排序检索数据（ORDER BY）

`ORDER BY`子句只能作为`SELECT`最后一条子句

```SQL
#单列排序
SELECT col
FROM table_name
ORDER BY col;

#多列排序
SELECT col1,col2,col3
FROM table_name
ORDER BY col2,col3;

#按照相对位置排序
SELECT col1,col2(2),col3(3)
FROM table_name
ORDER BY 2,3;

#按照降序进行排列，即从大到小；一般情况默认为升序
SELECT col1,col2,col3
FROM table_name
ORDER BY col2 DESC,col3;#若想每一列按照降序排列，则均要指定 DESC
```

## 第 4 章 过滤数据

`WHERE`子句用来筛选特定的行
`WHERE`子句接在`FROE`子句之后
`WHERE`子句操作符见《SQL 必知必会》P31

```SQL
#过滤单列
SELECT col1,col2,col3,...,col4
FROM tables
WHERE col1<>1.0;

#检查某个范围
SELECT col1,col2,col3,...,col4
FROM tables
WHERE col1 BETWEEN 1.0 AND 5.0;

#检查空值
SELECT col1,col2,col3,...,col4
FROM tables
WHERE coln IS NULL;
```

## 第 5 章 高级数据过滤

- 多个 WHERE 子句

AND 要求所有条件同时成立
OR 当第一个条件满足时，就不再计算第二个条件了，满足任意一个条件即可
WHERE 子句可以包括多个 AND 和 OR 子句
优先级：「()」>AND>OR

```sql
SELECT col1,col2,...,coln
FROM table
WHERE condition1 < 2.0 AND/OR condition2 != 5.0;
```

- 使用 IN 操作符

在圆括号中指定匹配值
IN 中同样可以使用 SELECT 子句

```sql
SELECT col1,col2,...,coln
FROM table
WHERE col4 in ("condition1","condition2",...,"conditionn");
```

- NOT 操作符
否定要过滤的列之后的关键字

```
SELECT col1,col2,...,coln
FROM table
WHERE NOT col4 = "ABCD"
ORDER BY col1;
```

## 第 6 章 用通配符过滤数据

用来匹配一部分特殊字符、特殊模式，区分大小写
用来匹配一个字段的值，是完整的

- LIKE 操作符
1. `%` 表示任意字符出现任意次数
2. `\_` 只匹配单个字符
3. `[ ]` 用来匹配指定位置的指定字符集的任意一个字符  
4. 不要过度使用通配符
5. 不要将通配符置于匹配模式开头

```sql
SELECT col1,col2,...,coln
FROM table
WHERE col3 LIKE '%Fish%';
WHERE col3 LIKE '_Fish__';
WHERE col3 LIKE '[A^CV]%'; #匹配任意以A、V之后的任意数目字符
WHERE NOT col3 LIKE '[ACV]%';
```

## 第 7 章 创建计算字段

由原有的 field 计算新的 field

```sql
SELECT col1 || col2 # 将两个字段拼接 Postgresql
SELECT Concat(col1,col2) #MySql 连接字段的函数
FROM table;
```

对字段使用「TRIM LTRIM RTRIM」函数， 分别去掉字符串左右两边、左边、右边的空格
使用关键字 `AS`(alias) 将计算字段得到的值用新字段命名

```sql
SELECT Concat(TRIM(col1),col2) AS newcol # MySql 连接字段的函数
FROM table;
```

对 field 进行普通运算

```sql
SELECT col1*col2 AS newcol
FROM table
WHERE col3 10.0 between 20.0;
```

## 第 8 章 使用函数处理数据

文本处理、
数值运算、
日期-时间：提取日期成分、比较日期、执行基于日期的运算、选择日期格式

```sql
SELECT func1(col1) AS newcol1,func2(col2) AS newcol2
FROM table
WHERE func3(col1) = func3('string')
```

## 第 9 章 汇总数据

聚集函数（aggregate function）：
汇总数据而不是将其检索出来，**聚合函数不能用于 `WHERE` 子句**
```
AVG()：只能作用于一列，返回该列的平均值
COUNT()：COUNT(\*)对表中行数进行统计，COUNT(col)统计一列行数
MAX() MIN()：返回该列的最大值/最小值
SUM()：求和
DISTINCT 不能用于 COUNT(*) & 表达式
```

```sql
SELECT AVG /COUNT /MAX /MIN /SUM(DISTINCT col / *) AS new_col
FROM table
WHERE condition
```

## 第 10 章 分组数据 

- GROUP 子句

1. GROUP BY 子句可附带任意数目的列
2. GROUP BY 子句嵌套了分组， 则将在最后指定的分组上汇总
3. SELECT 的每一列要么在 GROUP BY 子句中给出，要么就被包含到聚集函数中
4. SELECT 中使用了表达式（不能使聚集函数），那么 GROUP BY 则必须使用同样的表达式
5. WHERE > GROUP BY > ORDER BY

```sql
SELECT col1,col2
FROM tables
WHERE cond1
GROUP BY col1,col2 #在 col2 上进行汇总
ORDER BY col3
```

- HAVING 子句

1. WHERE 子句在数据分组之前过滤
2. HAVING 子句在数据分组之后过滤，结合 GROUP BY 使用
3. HAVING 子句中可使用聚合函数

```sql
SELECT col1,col2,COUNT(*) AS newcol3
FROM tables
WHERE col4 > 4.0
GROUP BY col1 #在 newcol3 上进行汇总
HAVING COUNT(*) > 6;
```

- GROUP BY 与 ORDER BY 之间的差别

todo

## 第 11 章 使用子查询 -- 嵌套在查询中的其他查询

子查询总是从内到外处理
子查询只能查询单列

- 使用子查询进行过滤，作为`WHERE`子句的一部分
```sql
SELECT col1,col2
FROM table1
WHERE col3 IN (SELECT col3
               FROM table2
               WHERE condition);
```

- 使用子查询创建`SELECT`的字段

```SQL
SELECT
      col1,
      col2,
      (SELECT COUNT(*)
       FROM table2
       WHERE condition2) AS newcol3
FROM table1
WHERE condition1
GROUP BY col1
HAVING newcol3 > 1.0
ORDER BY col2;
```

- 子查询的结果作为`FROM`查询范围

```sql
SELECT S.*,B.MAXD 
FROM SCORES AS S, (SELECT SNO,MAX(DEGREE) AS MAXD 
       FROM SCORES
       GROUP BY SNO 
       HAVING COUNT(*)>1 ) AS B 
WHERE S.SNO=B.SNO 
AND S.DEGREE<B.MAXD 
ORDER BY SNO; 
```

- 完全限定列名避免歧义

**table_name.col_name**

## 第 12 章 联结(join)表

需要继续学习数据库原理

关系表的设计就是要把信息分解为多个表。通过某些共同的值互相关联。

创建联结，指定要联结的表以及联结的方式。若没有在 WHERE 子句中指定联结方式则作笛卡尔积。

- 内联结(等值联结)

```sql
SELECT col1,col2,col3...coln
FROM table1,table2
WHERE table1.col4 = table2.col4
```
或者
```SQL
SELECT col1,col2,col3
FROM table1 INNER JOIN table2
ON table1.col4 = table2.col4 and condition3;
```

- 联结多个表 & 普通过滤

```sql
SELECT col1,col2,col3...coln
FROM table1,table2,table3
WHERE table1.col3 = table2.col3
AND table2.col5 = table3.col5
AND col7 = "XXX";
```

```sql
select * 
from ( ((A inner join B on A.a = B.b)
inner join C on C.c = A.a)
inner join D on D.d = C.c)
inner join E on E.e = D.d;
```


## 第 13 章 创建高级联结

- 给表起别名 table AS new_table_name
可用于 WHERE 子句、ORDER BY 子句、SELECT 列表
```sql
SELECT col1,col2,col3...coln
FROM table1 AS t1,table2 AS t2
WHERE t1.col3 = t2.col3;
```
- 自联结(self-join)
使用别名，同一张表与自身做联结
```sql
SELECT c1.col1,c1.col2,c1.col3
FROM table1 AS c1,table1 AS c2
WHERE c1.col2 = c2.col2
AND C2.col3 = "XXXX";
```

- 自然联结(natural-join)

内联结（等值联结）是自然联结。自然联结排除多次出现，使得每一列只返回一次
```sql
SELECT t1.*,#通配符只对第一个表有用
       t2.col2,t2.col3,t2.col3,
       t3.col4,t3.col5,t3.col6,
FROM table1 AS t1,table2 AS t2，table3 AS t3
WHERE t1.col1 = t2.col4
AND   t2.col3 = t3.col5
AND   t1.col2 = "XXXXX";
```

- 外联结(outer-join)

将一个表中的行与另一个表中的行相关联，但有时候需要包含没有关联行的那些行。

```SQL
SELECT table1.col1,table2.col2
FROM table1 LEFT OUTER JOIN table2 # 指定包括所有行的表 左边
FROM table1 RIGHT OUTER JOIN table2 # 指定包含所有行的表 右边
ON table1.col4 = table2.col4;
```

- 使用带有聚集函数的联结，需要搭配 GROUP BY 子句

```SQL
SELECT table1.col1,
       COUNT(table2.col2) AS newcol2
FROM table1 INNER JOIN table2
ON table1.col4 = table2.col4
GROUP BY table1.col1;
```

## 第 14 章 组合(UNION)查询

UNION 操作符

1. 将多条 SELECT 查询语句组合成一个结果集
2. 将复杂的过滤条件分解为较简单的的条件
3. 必须有两条以上 SELECT 语句，其中每个查询必须包含相同的列、表达式或聚集函数
4. 从查询结果集中自动去除了重复的行，UNION ALL 返回所有匹配行
5. 只能有一个 ORDER BY 子句，放在最后一条 SELECT 语句
```sql
SELECT col1,col2,col3
FROM table1
WHERE condition1
UNION
SELECT col1,col2,col3
FROM table1
WHERE condition2
ORDER BY col2，col3；
```

- - -

# 四、高级特性

## 第 18 章 使用视图

包含动态检索时的数据的查询、简化复杂的联结、使用的是表的一部分、创建可重复使用 、禁止在视图查询中使用 ORDER BY 子句// 视图的规则和限制详细见 P157 18.1.2 //创建视图 CREATE VIEW view_name AS [只能有一条]SELECT 子句 // 删除视图 DROP VIEW view_name // 使用视图

## 第 19 章 使用存储过程

 为了以后使用而保存一条或者多条 SQL 语句，可视为批处理文件 // 使用存储过程 的理由 P167 // 执行储存过程 EXECUTE [ 储存过程的名字 ] //创建储存过程，【查看不同 DBMS 文档关于创建储存过程】 Oracle 版本 CREATE PROCEDURE procedure_name( ListCount IN /

## 第 20 章 管理事务处理

管理事务处理(transaction processing) 用来管理成批执行的 SQL 操作 保证数据库不包含不完整的操作结果 // 事务 transaction 指的是一组 SQL 语句 // 回退 rollback 撤销指定 SQL 语句的过程 ,可回退 INSERT/ UPDATE/ DELETE。DELETE FROM table_name;ROLL

## 第 21 章 游标

使用游标(cursor / step) ,是一个存储在 DBMS 服务器上的数据集查询，不同的 DBMS 不同 1.声明游标 ：定义使用的 SELECT 语句和游标选项 2.声明后，必须打开使用 3. 使用后必须关闭游标。定义游标： DECLARE CURSOR cursor_name IS SELCT 子句 / 打开游标,执行查询，储存查询的数据以供浏览： O

## 第 22 章 高级 SQL 特性

### 约束
### 索引
### 触发器


约束{constraint} : 定义主键[PRIMARY KEY] CREATE TABLE table(col1 CHAR(10) NOT NULL PRIMARY KEY);或者 ALTER TABLE tables ADD CONSTRAINT PRIMARY KEY (col1); // 外键[REFERENCES] CREATE TA

# 参考资料：

1. 《SQL 必知必会》