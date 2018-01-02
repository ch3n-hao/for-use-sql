[TOC]

- - -

# 零、创建数据库、表的结构

## 第 17 章 创建、更新、删除、重命名表的结构(table)

- - -

- 创建表 

```

CREAT TABLE table_name

(        col1 该列数据类型 NOT NULL / NULL ,

​        col2 该列数据类型 NOT NULL / NULL,

​        col3 该列数据类型 ，

​        col3 该列数据类型 NOT NULL DEFUALT 10

); 

```

- - -

- 更新表 

增加字段、删除字段

尽可能减少对表结构的修改，在设计数据库的时候，尽可能更改表考虑

```

ALTER TABLE table_name

ADD col_name 该列数据类型；

ALTER TABLE table_name

DROP COLUMN col_name;

```

- - -

- 更加复杂的表结构更新

1. 创建一个新结构的表

2. 使用`INSERT SELECT`语句将旧表移动到新表

3. 检验新表中的数据

4. 旧表删除，如果需要的话

5. 重命名新表

6. 根据需求，添加SQL的高级特性

- - -

- 删除表 

```

DROP TABLE table_name;

```

- - -

- 重命名表 **此处有待根据使用的数据系统确定** 

```

RENAME old_table_name new_table_table

```

- - -

# 一、增

## 第 15 章 插入数据

- 将数据以行的形式插入至数据表中
  `INSERT` 插入一行
  `INSERT SELECT`插入多行

1. 插入完整的行

```
  # 这种写法，插入的数据依赖于表定义的结构，数据由`VALUES`给出，不是很安全，避免使用
  INSERT INTO table_name
  VALUES(col1_data,
         col2_data,
         col3_data,
         col4_data,
         NULL); 
```

```
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

```
# 插入部分行，省略其中的某些字段，该字段必须满足允许`NULL`值或给出默认值
  INSERT INTO table_name(col1,
                         col2,
                         col3 NULL 
                         col4,
                         col5 DEFUALT 10)
  VALUES(col1_data,
         col2_data,

         col4_data,
         NULL); 
```

3. 插入查询语句的结果

```
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

```
SELECT *
INTO table2
FROM table1;
```

- - -

# 二、删 & 改

## 第 16 章 更新和删除数据(行 & 列)

- 更新表中特定的行
- 更新表中所有的行

```
#更新语句结构
要更新的表，总是以要更新的表名开始
列名和他们的新值,以`SET`子句进行设置,新值可以使用子查询
确定要更新行的conditions,以`WHERE`子句结束
```

```
UPDATE table_name
SET col1 = new_value1,
    col2 = new_value2,
    ...
    coln = new_value3
WHERE  another = conditions;
```

- - -

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

```
DELETE FROM table_name
WHERE col = conditions;
```

/- - -

- 以上更新、删除语句均携带了`WHERE`子句，若无，则更新或者删除表中的所有行
- 每个表中都有主键，在`WHERE`中尽量使用他
- 在进行更新或者删除操作前，先用`SELECT`测试过滤`conditons`

- - -

# 三、查

## 第 1 章

SELECT[返回的列或者表达式] -> FROM[要求检索的表] -> WHERE[行级过滤] -> GROUP BY[无序分组] -> HAVING[组级过滤] -> ORDER BY[有序分组] -> LIMIT n1 OFFSET n2[限制从 n2 行起返回 n1 行] // 内联结 自联结 自然联结 交叉联结 左 右 全外联结 // **每条 SQL 语句以 `; `结束

## 第 2 章 检索数据 

```

SELECT DISTINCT cols 

FROM table LIMIT n1 OFFSET n2 (排除重复的值)

```

## 第 3 章 排序检索数据 

```

SELECT 

ORDER BY (DESC ENDING)

```

## 第 4 章 过滤数据 

```

SELECT columns 

FROM tables 

WHERE 子句操作符(BETWEEN / IS NULL )

```

## 第 5 章 高级过滤数据 

```

SELECT col 

FROM tab WHERE cond1 AND/OR con2 // 

WHERE col in (cond1,cond2...) 

```

IN&OR 作用类似 // NOT 否定之后的关键字

## 第 6 章 用通配符过滤数据 

WHERE cols LIKE '% _ [ ]'

## 第 7 章 创建计算字段 

由原有的 field 计算新的 field 

```

SELECT col1 +col2 +TRIM(col3) AS new_titles 

FROM table // 

```

“TRIM LTRIM RTRIM" 分别 去掉字符串左右、左边、右边的空格 别名AS alias // SELECT col1,col2,col3,col1*col

## 第 8 章 使用函数处理数据 

文本处理、数值运算、日期-时间 

```

SELECT col1,col2 

FROM table 

WHERE fun1(col1) = fun1('string')

```

## 第 9 章 汇总数据 

```SELCT AVG /COUNT /MAX /MIN /SUM(DISTINCT col / *) AS new_col 

FROM table WHERE condition 

DISTINCT 不能用于 COUNT(*) & 表达式 

```

SELECT AVG(col1) AS new

```

## 第 10 章 分组数据 

```

SELCET col1,col2 

FROM tables WHERE cond1 

GROUP BY col1,col2 ORDER BY col3 

```

GROUP BY 子句可嵌套分组，则在最后指定的分组汇总 

SELECT 中使用了表达式，那么 GROUP BY 则必须使用同样的表达式 // 

ORDER BY 分组排序 // 

HAVING

## 第 11 章 使用子查询 -- 嵌套在其他查询中的查询 

- 使用子查询进行过滤 

```

SELCET col1,col2 

FROM table1 WHERE col3 IN (SELCET col3 

FROM table2 WHERE cond1) 

```

-使用子查询创建计算字段 

```

SELECT col1,col2,(SELECT COUNT(*) FROM table2

```

## 第 12 章 联结(join)表 

-内联结(等值联结)

```

SELECT col1,col2,col3...n 

FROM table1,table2...n WHERE table1.col4 = table2.col4 或者 SELECT col1,col2,col3 FROM table1 INNER JOIN table2 ON table1.col4 = table2

```

## 第 13 章 创建高级联结表,自联结(self-join)、自然联结(natural-join)、外联结(outer-join) 

// 给表起别名 ....FROM table1 AS new_name1,table2 AS new_name2 // 自联结 ==> SELECT c1.col1,c1.col2,c1.col3 FROM table1 AS c1,tabl

## 第 14 章 组合(UNION)查询 

SELCET1 UNION(自动去除重复的行)/UNION ALL(返回所有重复的行) SELECT2.... OEDER BY [只能使用一条，作用于所有 SELECT 语句] //

- - -

# 四、高级特性

## 第 18 章 

使用视图 包含动态检索时的数据的查询、简化复杂的联结、使用的是表的一部分、创建可重复使用 、禁止在视图查询中使用 ORDER BY 子句// 视图的规则和限制详细见 P157 18.1.2 //创建视图 CREATE VIEW view_name AS [只能有一条]SELECT 子句 // 删除视图 DROP VIEW view_name // 使用视图

## 第 19 章 使用存储功能

 为了以后使用而保存一条或者多条 SQL 语句，可视为批处理文件 // 使用存储过程 的理由 P167 // 执行储存过程 EXECUTE [ 储存过程的名字 ] //创建储存过程，【查看不同 DBMS 文档关于创建储存过程】 Oracle 版本 CREATE PROCEDURE procedure_name( ListCount IN /

## 第 20 章 管理事务处理

管理事务处理(transaction processing) 用来管理成批执行的 SQL 操作 保证数据库不包含不完整的操作结果 // 事务 transaction 指的是一组 SQL 语句 // 回退 rollback 撤销指定 SQL 语句的过程 ,可回退 INSERT/ UPDATE/ DELETE。DELETE FROM table_name;ROLL

## 第 21 章 游标

使用游标(cursor / step) ,是一个存储在 DBMS 服务器上的数据集查询，不同的 DBMS 不同 1.声明游标 ：定义使用的 SELECT 语句和游标选项 2.声明后，必须打开使用 3. 使用后必须关闭游标。定义游标： DECLARE CURSOR cursor_name IS SELCT 子句 / 打开游标,执行查询，储存查询的数据以供浏览： O

## 第 22 章 高级 SQL 特性 

约束{constraint} : 定义主键[PRIMARY KEY] CREATE TABLE table(col1 CHAR(10) NOT NULL PRIMARY KEY);或者 ALTER TABLE tables ADD CONSTRAINT PRIMARY KEY (col1); // 外键[REFERENCES] CREATE TA

# 参考资料：

1. 《SQL 必知必会》