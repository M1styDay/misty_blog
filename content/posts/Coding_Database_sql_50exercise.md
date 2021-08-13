---
title: SQL_50 Exercise
author: "Misty"
tags: ["Database"]
categories: ["Coding"]
date: 2020-12-30
---

## 材料

### 题源+数据

[SQL面试必会50题](https://zhuanlan.zhihu.com/p/43289968)

### 表关系

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/0-%E8%A1%A8%E5%85%B3%E7%B3%BB.png)

---

## 题解

### 01-10

#### 1. 查询课程编号为“01”的课程比“02”的课程成绩高的所有学生的学号
```sql
SELECT st.s_id, a.s_score, b.s_score
FROM student st
INNER JOIN (SELECT s_id, s_score FROM score WHERE c_id = "01") as a on a.s_id = st.`s_id`
INNER JOIN (SELECT s_id, s_score FROM score WHERE c_id = "02") as b on b.s_id = st.`s_id`
WHERE a.s_score > b.s_score;
```

#### 2. 查询平均成绩大于60分的学生的学号和平均成绩
```sql
SELECT distinct s_id, AVG(s_score) as avg1 
FROM score
Group by S_id
having avg1 > 60
```

#### 3. 查询所有学生的学号、姓名、选课数、总成绩
```sql
SELECT student.s_id, student.s_name, COUNT(c_id) as number, SUM(s_score) as sum
FROM student
INNER JOIN score
ON student.s_id = score.s_id
GROUP BY s_id;
```

#### 4. 查询姓“李”的老师的个数
```sql
SELECT COUNT(t_name)
FROM Teacher
WHERE t_name like "李%"
```

#### 5. 查询没学过“张三”老师课的学生的学号、姓名
```sql
SELECT s_id, s_name 
FROM student
WHERE s_id not in
(SELECT s_id FROM score WHERE c_id in
	(SELECT c_id FROM Course WHERE t_id in
		(SELECT T_id FROM Teacher WHERE t_name = "张三")))
```

#### 6. 查询学过“张三”老师所教的所有课的同学的学号、姓名
```sql
SELECT s_id, s_name 
FROM student
WHERE s_id in
(SELECT s_id FROM score WHERE c_id in
	(SELECT c_id FROM Course WHERE t_id in
		(SELECT T_id FROM Teacher WHERE t_name = "张三")))
```

#### 7. 查询学过编号为“01”的课程并且也学过编号为“02”的课程的学生的学号、姓名

解法一：

```sql
select distinct student.s_id, s_name
from student
where student.s_id in (
select distinct a.s_id 
from score a
inner join score b
on a.s_id = b.s_id
where a.c_id = '01' and b.c_id = '02')
```

解法二：

```sql
SELECT s_id, s_name 
FROM student
WHERE s_id IN 
(SELECT a.s_id 
FROM (SELECT s_id FROM score WHERE c_id = "01" ) a
WHERE s_id in (SELECT s_id FROM score WHERE c_id = "02")
)
```

解法三：

```sql
select student.s_id, student.s_name
from student 
where student.s_id in 
(select a.s_id from
(select score.s_id from score where c_id = '01') a,
(select score.s_id from score where c_id = '02') b
where a.s_id = b.s_id
)
```

#### 8. 查询课程编号为“02”的总成绩
```sql
SELECT SUM(s_score)
FROM Score
WHERE c_id = "02"
GROUP BY c_id
```

#### 9. 查询所有课程成绩小于60分的学生的学号、姓名
```sql
SELECT s_id, s_name
FROM student
WHERE s_id not in
(select distinct s_id from score where s_score > 60)
```

#### 10. 查询没有学全所有课的学生的学号、姓名

解法一：

```sql
select student.s_id, s_name
from student
left join score
on student.s_id = score.s_id
group by s_id
having count(score.c_id) !=
(select count(*)
from course)
```

解法二：

```sql
SELECT st.s_id , st.s_name
FROM student st 
INNER JOIN score sc 
ON st.s_id = sc.s_id 
GROUP BY st.s_id
HAVING COUNT(c_id) < (SELECT COUNT(DISTINCT c_id) FROM Course)
```

### 11-20

#### 11.查询至少有一门课与学号为“01”的学生所学课程相同的学生的学号和姓名

解法一：

```sql
select student.s_id, student.s_name
from student 
where student.s_id in
(select s_id from score where c_id in
(select c_id from score where s_id = '01') and s_id !='01')
```

解法二：
```sql
select distinct student.s_id, student.s_name
from student
inner join score on student.s_id = score.s_id
where c_id in (select c_id from score where score.s_id = '01') and score.s_id != '01'
```

#### 12.查询和“01”号同学所学课程完全相同的其他同学的学号

```sql
select s_id from score
where s_id not in
(select s_id from score where c_id not in (
select c_id from score where s_id = '01'))

and s_id != '01'

group by s_id
having count(distinct c_id) = (select count(distinct c_id) FROM score where s_id = "01")
```

#### 13.查询没学过"张三"老师讲授的任一门课程的学生姓名

```sql
SELECT s_id, s_name
From Student
WHere s_id not in(
SELECT score.s_id 
From Score
INNER JOIN Course ON score.c_id = course.c_id
INNER JOIN Teacher ON course.t_id = teacher.t_id
WHERE teacher.t_name = "张三")
```
#### 15.查询两门及其以上不及格课程的同学的学号，姓名及其平均成绩

```sql
select student.s_id, student.s_name, AVG(s_score)
from student 
inner join score
on student.s_id = score.s_id
where score.s_id in

(select distinct s_id
from score
where s_score < 60)
group by s_id
having count(c_id) >=2
```

也可以用where not替换where in查找不及格。

#### 16.检索"01"课程分数小于60，按分数降序排列的学生信息

```sql
SELECT *
FROM Student
INNER JOIN Score on Student.s_id = Score.s_id
WHERE s_score < 60 and c_id = "01"
Order by s_score DESC
```

#### 17.按平均成绩从高到低显示所有学生的所有课程的成绩以及平均成绩

```sql
select s_id,
MAX(case when c_id = '01' then s_score else null end) as "语文",
MAX(case when c_id = '02' then s_score else null end) as "数学",
MAX(case when c_id = '03' then s_score else null end) as "英语",
avg(s_score)
from score
group by s_id
Order by avg(s_score) desc
```

#### 18.查询各科成绩最高分、最低分和平均分

#以如下形式显示：课程ID，课程name，最高分，最低分，平均分，及格率，中等率，优良率，优秀率

#及格为>=60，中等为：70-80，优良为：80-90，优秀为：>=90

```sql
select score.c_id, c_name, max(s_score), min(s_score), avg(s_score),
avg(case when s_score>=60  then 1 else 0 end) as '及格率',
avg(case when s_score>= 70 and s_score<=80 then 1 else 0 end) as '中等率',
avg(case when s_score>= 80 and s_score<= 90 then 1 else 0 end) as '优良率',
avg(case when s_score>=90 then 1 else 0 end) as '优秀'
from score
inner join course
on score.c_id = course.c_id
group by score.c_id
```

#### 19.按各科成绩进行排序，并显示排名
#row_number() over (order by 列 desc)

```sql
SELECT s_id, c_id, s_score, row_number() over (order by s_score desc)
FROM score
```


#### 20.查询学生的总成绩并进行排名

```sql
select s_id, sum(s_score), row_number() over (order by sum(s_score) desc)
from score
group by s_id
```

### 21-30

#### 21.查询不同老师所教不同课程平均分从高到低显示

```sql
SELECT course.t_id, t_name, score.c_id, AVG(s_score)
FROM score
inner join course on score.c_id = course.c_id
inner join teacher on course.t_id = teacher.t_id
GROUP BY c_id
ORDER BY AVG(s_score) DESC
```

#### 22.查询所有课程的成绩第2名到第3名的学生信息及该课程成绩

```sql
SELECT *
FROM (SELECT score.s_id, student.s_name, score.c_id, score.s_score, row_number() over(partition by c_id order by s_score DESC) rank1
FROM score 
INNER JOIN student
ON score.s_id = student.s_id) a
WHERE rank1 in (2,3)
```
#### 23.使用分段来统计各科成绩，分别统计各分数段人数：课程ID和课程名称

```sql
SELECT score.c_id, course.c_name,
sum(case when score.s_score <= 100 and score.s_score > 85 then 1 else 0 end) as '[100-85]',
sum(case when score.s_score <= 85 and score.s_score > 70 then 1 else 0 end) as '[85-70]',
sum(case when score.s_score <= 70 and score.s_score > 60 then 1 else 0 end) as '[70-60]',
sum(case when score.s_score <= 60 and score.s_score > 0 then 1 else 0 end) as '[<60]'
FROM Score
INNER JOIN course on score.c_id = course.c_id
GROUP BY c_id
```

#### 24.查询学生平均成绩及其名次

row_number() over (order by 列 desc)

```sql
SELECT s_id, avg(s_score), row_number() over (order by avg(s_score) desc)
FROM score
Group by s_id
```

#### 25.查询各科成绩前三名的记录（不考虑成绩并列情况）

```sql
SELECT c_id, 
max(case when rank1 = 1 then s_score else null end ) as '第一',
max(case when rank1 = 2 then s_score else null end ) as '第二',
max(case when rank1 = 3 then s_score else null end ) as '第三'
FROM (SELECT score.s_id, student.s_name, score.c_id, score.s_score, row_number() over(partition by c_id order by s_score DESC) rank1
FROM score 
INNER JOIN student
ON score.s_id = student.s_id) a
WHERE rank1 in (1,2,3)
Group by c_id;
```

#### 26.查询每门课程被选修的学生数

```sql
select c_id, count(s_id) as '每门课选修的学生数'
FROM score
GROUP BY c_id
```

#### 27.查询出只有两门课程的全部学生的学号和姓名

```sql
SELECT score.s_id, student.s_name, count(score.c_id) as '课程数'
FROM score
INNER JOIN student
ON score.s_id = student.s_id
GROUP BY s_id
Having count(score.c_id) = 2
```

#### 28.查询男生、女生人数

```sql
select s_sex, count(s_id)
from student
group by s_sex
```


#### 29.查询名字中含有"风"字的学生信息

```sql
select *
from student
where s_name like "%风%"
```

### 31-40


#### 31.查询1990年出生的学生名单

```sql
select *
from student
where year(s_birth) = 1990
```

```sql
select *
from student
where s_birth like '%1990%'
```

#### 32.查询平均成绩大于等于85的所有学生的学号、姓名和平均成绩

```sql
SELECT score.s_id, student.s_name, avg(s_score)
FROM score
INNER JOIN student
ON score.s_id = student.s_id
GROUP BY score.s_id
Having avg(s_score) > 85
```

#### 33.查询每门课程的平均成绩，结果按平均成绩升序排序，平均成绩相同时，按课程号降序排列

```sql
SELECT Score.c_id, c_name, avg(s_score)
FROM Score
INNER JOIN Course
ON Score.c_id = Course.c_id
GROUP BY c_id
ORDER BY avg(s_score) , c_id DESC
```

#### 34.查询课程名称为"数学"，且分数低于60的学生姓名和分数（不重点）

```sql
SELECT score.s_id, student.s_name, s_score
FROM student
INNER JOIN score
ON student.s_id = score.s_id
INNER JOIN course
ON course.c_id = score.c_id
WHERE c_name = '数学' and s_score < 60
```

#### 35.查询所有学生的课程及分数情况（重点）

```sql
#1.因为要选出需要的字段 用case when 当co.c_name='数学' then 可以得到对应的 sc.s_core
#2.因为GROUP UP 要与select 列一致，所以case when 加修饰max
#3.因为最后要展现出每个同学的各科成绩为一行，所以用到case

select s_id, 
max(case when c_name = '语文' then s_score else null end ) as '语文',
max(case when c_name = '数学' then s_score else null end ) as '数学',
max(case when c_name = '英语' then s_score else null end ) as '英语'
FROM score
INNER JOIN course
ON score.c_id = course.c_id
GROUP BY s_id
```

#### 36.查询任何一门课程成绩在70分以上的姓名、课程名称和分数（重点）

```sql
select s_name, c_name, s_score
from score
inner join course
on score.c_id = course.c_id
inner join student
on student.s_id = score.s_id
where s_score > 70
```


#### 37.查询不及格的课程并按课程号从大到小排列(不重点)

```sql
select score.s_id, s_name, c_id, s_score
from score
inner join student
on score.s_id = student.s_id
where s_score < 60
order by c_id 
```

#### 38.查询课程编号为03且课程成绩在80分以上的学生的学号和姓名

```sql
select score.s_id, s_name, c_id, s_score
from score
inner join student
on score.s_id = student.s_id
where c_id = '03' and s_score > 80
```

#### 39.求每门课程的学生人数
```sql
select score.c_id, c_name, count(s_id) as '人数'
from score
inner join course
on score.c_id = course.c_id
group by c_id
```

#### 40.查询选修“张三”老师所授课程的学生中成绩最高的学生姓名及其成绩（重要top）
```sql
select score.s_id, s_name, s_score
from score
inner join student
on score.s_id = student.s_id
inner join course
on score.c_id = course.c_id
inner join teacher
on teacher.t_id = course.t_id
where t_name = '张三'
order by s_score desc
limit 1 offset 1
```

### 41-50

#### 41.查询不同课程成绩相同的学生的学生编号、课程编号、学生成绩
```sql
select distinct a.s_id, a.c_id, a.s_score
from score a inner join score b
on a.s_id = b.s_id
where a.s_score = b.s_score and a.c_id != b.c_id
```

#### 42.查询每门功成绩最好的前两名
```sql
SELECT c_id, 
max(case when rank1 = 1 then s_score else null end ) as '第一',
max(case when rank1 = 2 then s_score else null end ) as '第二'
FROM (SELECT score.s_id, student.s_name, score.c_id, score.s_score, row_number() over(partition by c_id order by s_score DESC) rank1
FROM score 
INNER JOIN student
ON score.s_id = student.s_id) a
WHERE rank1 in (1,2)
Group by c_id;
```

#### 43.统计每门课程的学生选修人数（超过5人的课程才统计）。要求输出课程号和选修人数，查询结果按人数降序排列，若人数相同，按课程号升序排列（不重要）
```sql
select c_id, count(s_id)
from score
group by c_id
having count(s_id) > 5
order by count(s_id) desc , c_id
```

#### 44.检索至少选修两门课程的学生学号
```sql
select s_id
from (select s_id , count(c_id)
from score 
group by s_id
having count(c_id)>=2 ) a
```

#### 45.查询选修了全部课程的学生信息
```sql
select distinct *
from student
where s_id in 
(select s_id
from score
group by s_id
having count(c_id) = (select count(*) from course))
```

#### 46.查询没学过“张三”老师讲授的任一门课程的学生姓名
```sql
select s_name
from student
where student.s_id not in 
(select student.s_id
from student
inner join score on student.s_id = score.s_id
inner join course on score.c_id = course.c_id
inner join teacher on teacher.t_id = course.t_id
where t_name = "张三" )
```
 
#### 47.查询两门以上不及格课程的同学的学号及其平均成绩
```sql
select s_id, avg(s_score)
from (select s_id, c_id, s_score
from score
where s_score < 60) a
group by s_id
having count(c_id) >= 2
```

```sql
select s_id, avg(s_score), count(s_score)
from score
where s_score < 60
group by s_id 
having count(s_score) >=2
```

#### 48.查询各学生的年龄（精确到月份）

```sql
#年份转换成月份，比如结果是1.9，ditediff 最后取1年
select s_id, s_birth,
datediff('2021-1-9', s_birth)/365
from student
```

#### 49.查询本周过生日的学生

```sql
select *
from student
where week(s_birth, 1) = week(date(now()),1)

#查询下周过生日的学生
select *
from student
where week(s_birth, 1) = week(date(now()),1) +1
```


#### 50.查询本月过生日的学生
```sql
select *
from student
where month(s_birth) = month (date(now()))

#查询下月过生日的学生
select *
from student
where month(s_birth) = month (date(now()))+1
```







&nbsp; 

---

&nbsp; 

## Reference
Name|Link|Remarks
:---:|:---:|:---:
陆小亮|[【数据分析】- SQL面试50题](https://www.bilibili.com/medialist/play/ml1058913098/BV1q4411G7Lw)|Null