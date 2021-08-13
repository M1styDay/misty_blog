---
title: SQL_Note2
author: "Misty"
tags: ["Database"]
categories: ["Coding"]
date: 2020-12-28
---

## DDL & DML

### 库操作

#### 创建数据库

CREATE DATABASE database-name

#### 删除数据库

drop database dbname 

#### 分离数据库

sp_detach_db

#### 附加数据库

sp_attach_db （后接表明，附加需要完整的路径名）

#### 修改数据库名称

sp_renamedb 'old_name', 'new_name'

### 表操作

#### 创建新表

create table tabname(col1 type1 [not null] [primary key],col2 type2 [not null],..) 

#### 根据已有的表创建新表

A：create table tab_new like tab_old 

B：create table tab_new as select col1,col2… from tab_old definition only

#### 删除表

drop table tabname

#### 增加列

Alter table tabname add column col type

#### 添加/删除主键

Alter table tabname add primary key(col)

Alter table tabname drop primary key(col) 

#### 创建/删除索引（索引不可更改，想要改必须删除重新建）

create [unique] index idxname on tabname(col….) 

drop index idxname

#### 创建/删除视图

create view viewname as select statement

drop view viewname

### update & alter

#### update 语句可用来修改表中的数据

update 表名称 set 列名称=新值 where 更新条件

#### Alter 语句可用来修改数据表名或修改数据表字段

add/drop/change/modify/set default/rename

### insert/create & delete/drop

区别用法


---

## DQL

### 基础语法
选择：select * from table1 where 范围

插入：insert into table1(field1,field2) values(value1,value2)

删除：delete from table1 where 

范围更新：update table1 set field1=value1 where 范围

查找：select * from table1 where field1 like ’%value1%’

排序：select * from table1 order by field1,field2 [desc]

总数：select count as totalcount from table1

求和：select sum(field1) as sumvalue from table1

平均：select avg(field1) as avgvalue from table1

最大：select max(field1) as maxvalue from table1

最小：select min(field1) as minvalue from table1

### 高级查询运算词

A：UNION 运算符 

UNION 运算符通过组合其他两个结果表（例如 TABLE1 和 TABLE2）并消去表中任何重复行而派生出一个结果表。当 ALL 随 UNION 一起使用时（即 UNION ALL），不消除重复行。两种情况下，派生表的每一行不是来自 TABLE1 就是来自 TABLE2。

B：EXCEPT 运算符 

EXCEPT运算符通过包括所有在 TABLE1 中但不在 TABLE2 中的行并消除所有重复行而派生出一个结果表。当 ALL 随 EXCEPT 一起使用时 (EXCEPT ALL)，不消除重复行。

C：INTERSECT 运算符

INTERSECT运算符通过只包括 TABLE1 和 TABLE2 中都有的行并消除所有重复行而派生出一个结果表。当 ALL随 INTERSECT 一起使用时 (INTERSECT ALL)，不消除重复行。 
注：使用运算词的几个查询结果行必须是一致的。

### 外连接

A：left （outer） join

左外连接（左连接）：结果集几包括连接表的匹配行，也包括左连接表的所有行。 
SQL: select a.a, a.b, a.c, b.c, b.d, b.f from a LEFT OUT JOIN b ON a.a = b.c

B：right （outer） join

右外连接(右连接)：结果集既包括连接表的匹配连接行，也包括右连接表的所有行。


C：full/cross （outer） join

全外连接：不仅包括符号连接表的匹配行，还包括两个连接表中的所有记录。


### 分组（Group By）

一张表，一旦分组 完成后，查询后只能得到组相关的信息。

组相关的信息：（统计信息） count,sum,max,min,avg  分组的标准)

Group by + having

---

## 提升应用

#### 复制表(只复制结构,源表名：a 新表名：b)

select top 0 * into b from a

#### 拷贝表(拷贝数据,源表名：a 目标表名：b)

insert into b(a, b, c) select d,e,f from b

#### 跨数据库之间表的拷贝(具体数据使用绝对路径)

insert into b(a, b, c) select d,e,f from b in ‘具体数据库’ where 条件

例子：..from b in '"&Server.MapPath(".")&"\data.mdb" &"' where..

#### 子查询(表名1：a 表名2：b)

select a,b,c from a where a IN (select d from b ) 或者: select a,b,c from a where a IN (1,2,3)

#### 显示文章、提交人和最后回复时间

select a.title,a.username,b.adddate from table a,(select max(adddate) adddate from table where table.title=a.title) b

#### 外连接查询

select a.a, a.b, a.c, b.c, b.d, b.f from a LEFT OUT JOIN b ON a.a = b.c

#### 在线视图查询

select * from (SELECT a,b,c FROM a) T where t.a > 1;

#### between的用法：between限制查询数据范围时包括了边界值,not between不包括

select * from table1 where time between time1 and time2

select a,b,c, from table1 where a not between 数值1 and 数值2

#### in 的使用方法

select * from table1 where a [not] in (‘值1’,’值2’,’值4’,’值6’)

#### 两张关联表，删除主表中已经在副表中没有的信息 

delete from table1 where not exists ( select * from table2 where table1.field1=table2.field1 )

#### 四表联查问题

select * from a left inner join b on a.a=b.b right inner join c on a.a=c.c inner join d on a.a=d.d where .....

#### 日常安排提前五分钟提醒

select * from 日程安排 where datediff('minute',f开始时间,getdate())>5

#### 数据库分页

select top 10 b.* 

from (select top 20 主键字段,排序字段 from 表名 order by 排序字段 desc) a,表名 b 

where b.主键字段 = a.主键字段 

order by a.排序字段

#### 前10条记录

select top 10 * form table1 where 范围

#### 选择在每一组b值相同的数据中对应的a最大的记录的所有信息(类似这样的用法可以用于论坛每月排行榜,每月热销产品分析,按科目成绩排名,等等。)

select a,b,c from tablename ta where a=(select max(a) from tablename tb where tb.b=ta.b)

#### 包括所有在TableA中、但不在TableB和TableC中的行并消除所有重复行而派生出一个结果表

(select a from tableA ) except (select a from tableB) except (select a from tableC)

#### 随机取出10条数据

select top 10 * from tablename order by newid()

#### 随机选择记录

select newid()

#### 删除重复记录

delete from tablename where id not in (select max(id) from tablename group by col1,col2,...)

#### 列出数据库里所有的表名

select name from sysobjects where type='U' // U代表用户

#### 列出表里的所有的列名

select name from syscolumns where id=object_id('TableName')

#### 初始化表table1

TRUNCATE TABLE table1

#### 选择从10到15的记录

select top 5 * from (select top 15 * from table order by id asc) table_别名 order by id desc

&nbsp; 

---

&nbsp; 

## Reference
Name|Link|Remarks
:---:|:---:|:---:
小蚊子数据分析|[1500字sql语句大全](https://mp.weixin.qq.com/s/by_ZOQvLFTtpd7ciGh1b9w)|前半篇