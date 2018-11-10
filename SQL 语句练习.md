# SQL 语句练习——学生系列 
看完《sql 必知必会》想基于 Postgresql 做一些题目
题源：https://blog.csdn.net/mrbcy/article/details/68965271  

## 创建数据库
```sql
CREATE DATABASE database_name; # 创建数据库
```

## 创建数据表，并插入数据

```sql
CREATE TABLE students
(sno VARCHAR(3) NOT NULL, 
sname VARCHAR(4) NOT NULL,
ssex VARCHAR(2) NOT NULL, 
sbirthday DATE,
class VARCHAR(5))

INSERT INTO STUDENTS (SNO,SNAME,SSEX,SBIRTHDAY,CLASS) VALUES (108 ,'曾华' ,'男' ,'1977-09-01',95033);
INSERT INTO STUDENTS (SNO,SNAME,SSEX,SBIRTHDAY,CLASS) VALUES (105 ,'匡明' ,'男' ,'1975-10-02',95031);
INSERT INTO STUDENTS (SNO,SNAME,SSEX,SBIRTHDAY,CLASS) VALUES (107 ,'王丽' ,'女' ,'1976-01-23',95033);
INSERT INTO STUDENTS (SNO,SNAME,SSEX,SBIRTHDAY,CLASS) VALUES (101 ,'李军' ,'男' ,'1976-02-20',95033);
INSERT INTO STUDENTS (SNO,SNAME,SSEX,SBIRTHDAY,CLASS) VALUES (109 ,'王芳' ,'女' ,'1975-02-10',95031);
INSERT INTO STUDENTS (SNO,SNAME,SSEX,SBIRTHDAY,CLASS) VALUES (103 ,'陆君' ,'男' ,'1974-06-03',95031);
```

```sql
CREATE TABLE courses
(cno VARCHAR(5) NOT NULL, 
cname VARCHAR(10) NOT NULL, 
tno VARCHAR(10) NOT NULL)

INSERT INTO COURSES(CNO,CNAME,TNO)VALUES ('3-105' ,'计算机导论',825);
INSERT INTO COURSES(CNO,CNAME,TNO)VALUES ('3-245' ,'操作系统' ,804);
INSERT INTO COURSES(CNO,CNAME,TNO)VALUES ('6-166' ,'数据电路' ,856);
INSERT INTO COURSES(CNO,CNAME,TNO)VALUES ('9-888' ,'高等数学' ,100);
```

```sql
CREATE TABLE scores 
(sno VARCHAR(3) NOT NULL, 
cno VARCHAR(5) NOT NULL, 
degree NUMERIC(10, 1) NOT NULL) 

INSERT INTO SCORES(SNO,CNO,DEGREE)VALUES (103,'3-245',86);
INSERT INTO SCORES(SNO,CNO,DEGREE)VALUES (105,'3-245',75);
INSERT INTO SCORES(SNO,CNO,DEGREE)VALUES (109,'3-245',68);
INSERT INTO SCORES(SNO,CNO,DEGREE)VALUES (103,'3-105',92);
INSERT INTO SCORES(SNO,CNO,DEGREE)VALUES (105,'3-105',88);
INSERT INTO SCORES(SNO,CNO,DEGREE)VALUES (109,'3-105',76);
INSERT INTO SCORES(SNO,CNO,DEGREE)VALUES (101,'3-105',64);
INSERT INTO SCORES(SNO,CNO,DEGREE)VALUES (107,'3-105',91);
INSERT INTO SCORES(SNO,CNO,DEGREE)VALUES (108,'3-105',78);
INSERT INTO SCORES(SNO,CNO,DEGREE)VALUES (101,'6-166',85);
INSERT INTO SCORES(SNO,CNO,DEGREE)VALUES (107,'6-106',79);
INSERT INTO SCORES(SNO,CNO,DEGREE)VALUES (108,'6-166',81);
```

```sql
CREATE TABLE teachers 
(tno VARCHAR(3) NOT NULL, 
tname VARCHAR(4) NOT NULL, tsex VARCHAR(2) NOT NULL, 
tbirthday DATE NOT NULL, prof VARCHAR(6), 
depart VARCHAR(10) NOT NULL)

INSERT INTO TEACHERS(TNO,TNAME,TSEX,TBIRTHDAY,PROF,DEPART) VALUES (804,'李诚','男','1958-12-02','副教授','计算机系');
INSERT INTO TEACHERS(TNO,TNAME,TSEX,TBIRTHDAY,PROF,DEPART) VALUES (856,'张旭','男','1969-03-12','讲师','电子工程系');
INSERT INTO TEACHERS(TNO,TNAME,TSEX,TBIRTHDAY,PROF,DEPART) VALUES (825,'王萍','女','1972-05-05','助教','计算机系');
INSERT INTO TEACHERS(TNO,TNAME,TSEX,TBIRTHDAY,PROF,DEPART) VALUES (831,'刘冰','女','1977-08-14','助教','电子工程系');
```

```sql
create table grade(low number(3,0),upp number(3),rank char(1));

insert into grade values(90,100,’A’);
insert into grade values(80,89,’B’);
insert into grade values(70,79,’C’);
insert into grade values(60,69,’D’);
insert into grade values(0,59,’E’);
```

## 题目列表

1. 查询Student表中的所有记录的Sname、Ssex和Class列。
2. 查询教师所有的单位即不重复的Depart列。
3. 查询Student表的所有记录。
4. 查询Score表中成绩在60到80之间的所有记录。
5. 查询Score表中成绩为85，86或88的记录。
6. 查询Student表中“95031”班或性别为“女”的同学记录。
7. 以Class降序查询Student表的所有记录。
8. 以Cno升序、Degree降序查询Score表的所有记录。
9. 查询“95031”班的学生人数。
10. 查询Score表中的最高分的学生学号和课程号。
11. 查询‘3-105’号课程的平均分。
12. 查询Score表中至少有5名学生选修的并以3开头的课程的平均分数。
13. 查询最低分大于70，最高分小于90的Sno列。
14. 查询所有学生的Sname、Cno和Degree列。
15. 查询所有学生的Sno、Cname和Degree列。
16. 查询所有学生的Sname、Cname和Degree列。
17. 查询“95033”班所选课程的平均分。
18. 根据grade表：现查询所有同学的Sno、Cno和rank列。
19. 查询选修“3-105”课程的成绩高于“109”号同学成绩的所有同学的记录。
20. 查询scores中选学一门以上课程的同学中分数为非最高分成绩的记录。
21. 查询成绩高于学号为“109”、课程号为“3-105”的成绩的所有记录。
22. 查询和学号为108的同学同年出生的所有学生的Sno、Sname和Sbirthday列。
23. 查询“张旭“教师任课的学生成绩。
24. 查询选修某课程的同学人数多于5人的教师姓名。
25. 查询95033班和95031班全体学生的记录。
26. 查询存在有85分以上成绩的课程Cno.
27. 查询出“计算机系“教师所教课程的成绩表。
28. 查询“计算机系”与“电子工程系“不同职称的教师的Tname和Prof。
29. 查询选修编号为“3-105“课程且成绩至少高于选修编号为“3-245”的同学的Cno、Sno和Degree,并按Degree从高到低次序排序。
30. 查询选修编号为“3-105”且成绩高于选修编号为“3-245”课程的同学的Cno、Sno和Degree.
31. 查询所有教师和同学的name、sex和birthday.
32. 查询所有“女”教师和“女”同学的name、sex和birthday.
33. 查询成绩比该课程平均成绩低的同学的成绩表。
34. 查询所有任课教师的Tname和Depart.
35. 查询所有未讲课的教师的Tname和Depart. 
36. 查询至少有2名男生的班号。
37. 查询Student表中不姓“王”的同学记录。
38. 查询Student表中每个学生的姓名和年龄。
39. 查询Student表中最大和最小的Sbirthday日期值。
40. 以班号和年龄从大到小的顺序查询Student表中的全部记录。
41. 查询“男”教师及其所上的课程。
42. 查询最高分同学的Sno、Cno和Degree列。
43. 查询和“李军”同性别的所有同学的Sname.
44. 查询和“李军”同性别并同班的同学Sname.
45. 查询所有选修“计算机导论”课程的“男”同学的成绩表

## 解答

> 从第 20 题开始记录

20. 查询scores中选学一门以上课程的同学中分数为非最高分成绩的记录。
```sql
SELECT s1.sno, s1.cno, s1.degree
FROM (
	SELECT SNO,MAX(DEGREE) AS MAXDEGREE  -- 查询一名学生所学课程的最高分
	FROM SCORES 
	GROUP BY SNO) as s2,SCORES AS s1
WHERE s1.SNO IN (SELECT SNO 
                 FROM SCORES 
                 GROUP BY SNO 
                 HAVING COUNT(CNO)>1)  -- 至少学一门以上课程的学生
AND s1.sno = s2.sno
AND s1.DEGREE <> s2.MAXDEGREE
ORDER BY s1.sno
```

21. 查询成绩高于学号为“109”、课程号为“3-105”的成绩的所有记录。
```SQL
SELECT *
FROM SCORES
WHERE DEGREE > (SELECT DEGREE 
			 FROM SCORES
			 WHERE SNO = '109'
			 AND CNO = '3-105' )
```

22. 查询和学号为108的同学同年出生的所有学生的Sno、Sname和Sbirthday列
todo

23. 查询“张旭“教师任课的学生成绩
```sql
select s1.sno,s1.degree 
from teachers as t1,scores as s1,courses as c1
WHERE t1.tno = c1.tno
and c1.cno = s1.cno
and t1.tname = '张旭'

-- 或者使用 inner join

select s1.sno,s1.degree 
from teachers as t1 
inner join courses as c1 
on t1.tno = c1.tno
inner join scores as s1 
on c1.cno = s1.cno
and t1.tname = '张旭'
```

24. 查询选修某课程的同学人数多于5人的教师姓名。
```SQL
SELECT DISTINCT teachers.tname
FROM teachers,courses,scores
WHERE teachers.tno = courses.tno
AND courses.cno = scores.cno
AND scores.cno IN (
SELECT CNO
FROM SCORES 
GROUP BY scores.cno
HAVING COUNT(scores.sno)>5)
```

25. 查询95033班和95031班全体学生的记录
```sql
SELECT *
FROM students 
WHERE class in ('95033','95031')
--WHERE class ='95033' or class ='95031'
```

26. 查询存在有85分以上成绩的课程Cno
```sql
SELECT distinct cno
FROM scores 
WHERE degree > 85
```

27. 查询出“计算机系“教师所教课程的成绩表
```sql
select scores.sno,scores.cno,scores.degree
from scores 
inner join courses on courses.cno = scores.cno
inner join teachers on teachers.tno = courses.tno
and teachers.depart = '计算机系'
```

28. 查询“计算机系”与“电子工程系“不同职称的教师的Tname和Prof
```sql
select tname,prof 
from teachers
where depart in ('计算机系','电子工程系') 
and prof NOT IN(
                  SELECT t1.prof 
	              from teachers as t1 inner join teachers as t2 
	              on t1.prof = t2.prof
	              and t1.depart = '电子工程系'
	              and t2.depart = '计算机系'
)
```

29. 查询选修编号为“3-105“课程且成绩至少高于任意选修编号为“3-245”的同学的成绩的Cno、Sno和Degree,并按Degree从高到低次序排序。

```sql
SELECT Cno,Sno,Degree
FROM Scores
WHERE Cno='3-105' 
AND Degree > ANY( -- 学习到了 any 函数的使用
    SELECT Degree
    FROM Scores
    WHERE Cno='3-245')
ORDER BY Degree DESC;
```

30. 查询选修编号为“3-105”且成绩高于所有选修编号为“3-245”课程的同学的Cno、Sno和Degree.
```sql
SELECT Cno,Sno,Degree
FROM Scores
WHERE Cno='3-105' AND Degree > ALL( -- 学习到了 all 函数的使用
    SELECT Degree
    FROM Scores
    WHERE Cno='3-245')
ORDER BY Degree DESC;
```

31. 查询所有教师和同学的name、sex和birthday.
```sql
select sname as name,ssex as sex,sbirthday as birthday
from students
union 
select tname as name,tsex as sex,tbirthday as birthday
from teachers
```

32. 查询所有“女”教师和“女”同学的name、sex和birthday
```sql
select sname as name,ssex as sex,sbirthday as birthday
from students
where students.ssex = '女'
union 
select tname as name,tsex as sex,tbirthday as birthday
from teachers
where teachers.tsex = '女'
```

33. 查询成绩比该课程平均成绩低的同学的成绩表
```sql
select s1.*
from scores as s1,(select cno,avg(degree) as agdegree
                   from scores
	               group by cno) as s2
where s1.cno = s2.cno
AND S1.DEGREE<s2.agdegree
```

34. 查询所有任课教师的Tname和Depart
```sql
select tname,depart
from teachers inner join courses
on teachers.tno=courses.tno;

-- 另一种解法
SELECT Tname,Depart
FROM Teachers
WHERE Teachers.Tno in (
                       SELECT TNO
                       FROM COURSES
                       );
```

35. 查询所有未讲课的教师的Tname和Depart
```sql
select Tname,depart
from teachers
where teachers.tno not in (select tno
                           from courses);
```

36. 查询至少有2名男生的班号
```sql
SELECT class
FROM students
where ssex = '男'
GROUP BY class
HAVING COUNT(SNO)>=2;
```

37. 查询Student表中不姓“王”的同学记录
```sql
SELECT *
FROM students
WHERE SNO NOT IN (
                  SELECT SNO
	              FROM Students
	              WHERE SNAME LIKE '王_'
                  );
-- 优化的
SELECT *
FROM students
WHERE NOT sname LIKE '王_';
```

38. 查询Student表中每个学生的姓名和年龄
```sql
SELECT sname,(SELECT extract(year from now())-extract(year FROM sbirthday)) as age
FROM students;
```

39. 查询Student表中每个学生的姓名和年龄
```sql
SELECT max(sbirthday),min(sbirthday)
FROM students
```

40. 以班号和年龄从大到小的顺序查询Student表中的全部记录
```sql
SELECT *
FROM students
ORDER BY CLASS,Sbirthday
```

41. 查询“男”教师及其所上的课程
```sql
SELECT teachers.tno,teachers.tname,courses.cname
FROM teachers inner join courses
ON teachers.tno = courses.tno
WHERE tsex = '男'
```

42. 查询最高分同学的Sno、Cno和Degree列
```SQL
SELECT sno,cno,degree -- 取巧的解法
FROM scores
order by degree desc
LIMIT 1

-- 对题目的另一种理解，查询每门课程最高分的同学
SELECT s1.* 
FROM scores AS S1 INNER JOIN ( SELECT cno,MAX(DEGREE) AS MAXdegree 
							  FROM scores 
							  GROUP BY cno
							 ) AS S2 
ON s1.cno=s2.cno and s1.degree=s2.MAXdegree 
```

43. 查询和“李军”同性别的所有同学的Sname

```sql
SELECT Sname
FROM Students
WHERE Ssex in (SELECT Ssex 
			  FROM Students
			  WHERE Sname = '李军')
AND Sname != '李军' -- 排除本身
```

44. 查询和“李军”同性别并同班的同学Sname
```sql
-- 笨方法
SELECT Sname
FROM Students
WHERE Ssex =(SELECT Ssex
			 FROM Students
			 WHERE Sname = '李军' 
			 )
AND Class = (SELECT Class
             FROM Students
			 WHERE Sname = '李军')
AND Sname != '李军'

-- 将子查询转化为联结表，以性别、班级相同作为联结
SELECT s2.Sname
FROM Students AS s1 INNER JOIN Students AS s2
ON S1.Ssex = S2.Ssex
AND S1.class = S2.class 
AND S1.sno != S2.sno -- 在左、右表中筛选出在同一个同班、性别相同的两个人，不是同一个人
where S1.SNAME = '李军'
```

45. 查询所有选修“计算机导论”课程的“男”同学的成绩表
```sql
SELECT scores.*
FROM scores inner join students 
on (scores.sno = students.sno and students.ssex='男')
inner join courses 
on (scores.cno = courses.cno and courses.cname = '计算机导论')
```