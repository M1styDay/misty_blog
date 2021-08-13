---
title: SQL_Note1
author: "Misty"
tags: ["Database"]
categories: ["Coding"]
date: 2020-12-26
---

## 表操作
### 创建表
```sql
create table 表名（字段名称 字段类型 约束，……）
```

##### 字符类型
* character 字符串
    * char(size)  保存固定长度的字符串
    * varchar(n) 可变长度的字符_最多8000个字符
    * text 可变长度的字符串_最多2GB字符数据
* unicode 字符串
    * nchar(n) 固定长度的Unicode数据_最多4000个字符
    * nvarchar(n) 可变长度的Unicode数据_最多4000个字符
    * ntext 可变长度的Unicode数据_最多2GB字符数据
* Binary 类型
    * bit 允许0/1/null
    * binary(n) 固定长度的二进制数据_最多8000字节
    * varbinary(n) 可变长度的二进制数据_最多8000字节
    * image 可变长度的二进制数据_最多2GB
* Number 类型
    * tinyint 允许从0到255的所有数字
    * int 允许从-2,147,483,648到2,147,483,647的所有数字_占4字节
    * bigint -9,223,372,036,854,775,808到9,223,372,036,854,775,807范围内数字_占8字节
    * float 从-1.79E+308到1.79E+308的浮动精度数字数据
    * real 从-3.40E+38到3.40E+38的浮动精度数字数据
    * money 10进制货币数据
* Date 类型
    * datetime 从1753年1月1日到9999年年12月31日，精度为3.33毫秒_8bytes
    * date 仅储存日期。从0001年1月1日到9999年12月31日_3bytes
* 其他数据类型
    * uniqueidentifler 存储全局标识符（GUID）
    * xml 存储XML格式化数据_最多2GB
    * cursor 存储对用于数据库操作的指针的引用
* 常见的字符类型选择
    * 字符类型建议采用varchar/nvarchar数据类型
    * 全额货币建议采用money数据类型
    * 自增长标识建议采用bigint数据类型（int类型限制）
    * 时间类型建议采用datetime数据类型
    * 尽量不用text、ntext、image
    * 尽量不用xml、varchar(max)、nvarchar(max)

##### 不同数据库数据字符类型区别
* https://www.runoob.com/sql/sql-datatypes.html

##### 约束
* 创建表时，对表进行限定，保证之后插入表的数据的完整性和正确性
  
##### 约束种类
* primary key 主键
    * 非空且唯一
* not null 非空
* unique 唯一
* autoincrement 主键且增长 
    * 当主键为integer型，可以自增长
* foreign key 外键
    * 一张表的外键可以关联另外一张的主键，而保证数据的完整性
* check 约束用于限制列中的值的范围
    * 如：check（age>0)
* default 约束用于向列中插入默认值
    * 如：city varchar(255) default "Sandnes"

##### 实例
```sql
    create tables student(
    id integer primary key autoincrement, #主键且自增长
    name text not null, #非空
    age integer,
    gender text,
    email text unique, #唯一
    check(age > 0)
    );
```

### 更新表
#### 增加列: add
```sql
alter table stu add classname text;
```

#### 删除列: drop
```sql
alter table table_name drop column column_nameble;
```

#### 修改列类型: modify
```sql
alter table stu modify column gender text;
```

#### 修改列名: change
* 字段类型不能丢，change不光能改列名也能修改类型
```sql
alter table stu change column gender sex text
```
#### 修改表名: rename
```sql
alter table stu rename to student
```

### 查询表
#### show tables
* 查询当前的数据库下的所有表名称
#### desc 表名
* 查询表的详细信息

### 删除表 
* drop table

## 操作表中的数据
### 增
* insert into 表名（列名1，列名2……） values （'值1'，'值2'……）
* 如果是给所有的列增加数据，则列名可以省略

### 删

* delete from 表名 [where 条件]
* 如果不加条件，则将表中的数据全部删除
* 删除所有行 truncate table

### 改

* update 表名 set 列名= 值， 列2=值2，……[where 条件]

```sql
update scores set scores = scores+5 where scores <=95
```

### 克隆表

参考[review](https://www.m1sty.com/2020/database_sql_sentences/)中的例子

## 查询数据

```sql
    SELECT selection_list    #要查询的列名称
    From table_list               #要查询的表名称
    WHERE condition          #行条件
    GROUP BY grouping_columns       #对结果分组
    HAVING condition                           #分组后的条件
    ORDER BY sorting_columns         #对结果分组
    LIMIT offset_start, row_count      #结果限定
```

### select
#### 通配符号 *
```sql
select * from table
```
#### 别名 as
```sql
select column_name from table_name AS name;
```

#### 拼接 concat() 
函数使用说明：返回不同的非NULL 值数目。若找不到匹配的项，则COUNT(DISTINCT) 返回 0

```sql
select concat('工号为:'，FNumber，'的员工的幸福指数:'，FSalary/(FAge-21))
select concat_ws(':','1','2','3') from test ; 
```

#### 去除重复的记录 distinct
```sql
select distinct column_name, column_name from table_name
```

### 目标：from
#### 连接 join
**简单连接 inner join：如果表中有至少一个匹配，则返回行**
```sql
    select column_name(s)
    from table1
    inner join table2
    on table1.column_name = table2.column_name;
```

**全连接 full outer join：返回左右表中的所有记录**
```sql
    select column_name(s)
    from table1
    full outer join table2
    on table1.column_name = table.column_name;
```

**左连接 left join：如果表中有至少一个匹配，则返回行**

* left join关键字从左表（table1）返回所有的行，即使右表（table2）中没有匹配。如果右表中没有匹配，则结果为null。

&nbsp; 

**右连接 right join：即使左表中没有匹配，也从右表返回所有的行**

* right join关键字从右表（table2）返回所有的行，即使左表（table1）中没有匹配。如果左表中没有匹配，则结果为null。

### 过滤：where
* =、！=、<>、<、<=、>、>=
* between... and：>= 且 <=
* is null：判断是否为null
* in(set)：在某一集合内
```sql
    select * from emp where sal in (5000,2000,1500);
```
* and
* or
* not
```sql
select * from emp where not sal > 1500
```

* like
  
1. 任意字符 %

```sql
#选取name以“G”开头的所有客户
select * from websites where name like 'G%'；
```
2. 单个字符 _

```sql 
#选取name以“G”开始，然后是一个任意字符，然后是“o”，然后是一个任意字符，然后是“le”的
select * from website where name like 'G_o_le'
```

3. 字符集 [charlist] / 不在字符列中的任何单一字符 [^charlist]

```sql
select * from websites where name regexp '^[A-H]'
```



### 分组：group by
* 用于结合合计函数，根据一个或多个列对结果进行分组
```sql
select column_name, function(column_name) from table_name group by column_name;
```

* having对分组之后的数据进行筛选
```sql
    select deptno, AVG(sal) from emp
    where sal > 1200
    group by deptno
    having AVG(sal) > 2200
```

### 排序：order by
* 语句用于根据指定的列对结果集进行排序
```sql
order by column_name ASC|DESC;
```
* 返回结果限定：limit
```sql
limit m offset n，从第n行开始往后的m行
```
### 子查询
```sql
select *
from customers
where id in （select id from customers where salary > 4500)
```
### 组合查询：union
合并两个或多个select语句的结果
* 使用规则

union必须由两条或两条以上select语句组成，语句之间用union分隔

union中的每个查询必须包含相同的列、表达式或聚集函数

列数据类型必须兼容：类型不必完全相同，但必须是DBMS可以隐含转换的类型（例如，不同的数值类型或不同的日期类型）

* 使用场景

在一个查询中从不同的表返回结构数据

对一个表执行多个查询，按一个查询返回数据

* 语法
```sql
    select cus_name, cus_contact, cus_email
    from customers
    where cus_state IN ('IL', 'IN', 'MI')
    union
    select cus_name, cus_contact, cus_email
    from customers
    where cus_name IN ('111");
```

* union all union（union只会选取结果中不同的值，用union all可选择选取重复的值）
* union和union all的区别是,union会自动压缩多个结果集合中的重复结果，而union all则将所有的结果全部显示出来，不管是不是重复。
    * *Union：对两个结果集进行并集操作，不包括重复行，同时进行默认规则的排序；*Union在进行表链接后会筛选掉重复的记录，所以在表链接后会对所产生的结果集进行排序运算，删除重复的记录再返回结果。实际大部分应用中是不会产生重复的记录，最常见的是过程表与历史表UNION。
    * *Union All：对两个结果集进行并集操作，包括重复行，不进行排序；*如果返回的两个结果集中有重复的数据，那么返回的结果集就会包含重复的数据了。

### 集合函数
* aggregate函数：计算从列中取得的值，返回一个单一的值

AVG()

COUNT()

FIRST()

LAST()

MIN()

SUM()

* sql scalar函数:基于输入值，返回一个单一的值
  
UCASE():将某个字段转换为大写
```sql
    select ucase(column_name) from table_name 
    select ucase(name) as site_title, url from websites
```
LCASE(): 将某个字段转换为小写

MID():从某个文本字段提取字符
```sql
    select mid(colunm_name, start[,length]) from table_name
```
LEN():返回某个文本字段的长度

ROUND():对某个数值字段进行指定小数位数的四舍五入
```sql
    select round(column_name, decimals) from table_name
```

NOW():返回当前的系统日期和时间
```sql
select name, url, now() as date from websites;
```

FORMAT():格式化某个字段的显示方式
```sql
    select format(column_name, format) from table_name;
```

### case when

参考[习题](https://www.m1sty.com/2020/database_sql_50/)中的例子

## 其他
### 触发器
### 事务
### 索引
### 视图
* 索引：索引是对数据库表中一列或多列的值进行排序的一种结构，使用索引可快速访问数据库表中的特定信息。如果想按特定职员的姓来查找他或她，则与在表中搜索所有的行相比，索引有助于更快地获取信息。索引分为聚簇索引和非聚簇索引两种，聚簇索引是按照数据存放的物理位置为顺序的，而非聚簇索引就不一样了；聚簇索引能提高多行检索的速度，而非聚簇索引对于单行的检索很快。根据数据库的功能，可以在数据库设计器中创建三种索引：唯一索引、主键索引和聚集索引。
    * 唯一索引：唯一索引是不允许其中任何两行具有相同索引值的索引。当现有数据中存在重复的键值时，大多数数据库不允许将新创建的唯一索引与表一起保存。数据库还可能防止添加将在表中创建重复键值的新数据。例如，如果在employee表中职员的姓(lname)上创建了唯一索引，则任何两个员工都不能同姓。
    * 主键索引：数据库表经常有一列或多列组合，其值唯一标识表中的每一行。该列称为表的主键。在数据库关系图中为表定义主键将自动创建主键索引，主键索引是唯一索引的特定类型。该索引要求主键中的每个值都唯一。当在查询中使用主键索引时，它还允许对数据的快速访问。
    * 聚集索引：在聚集索引中，表中行的物理顺序与键值的逻辑（索引）顺序相同。一个表只能包含一个聚集索引。如果某索引不是聚集索引，则表中行的物理顺序与键值的逻辑顺序不匹配。与非聚集索引相比，聚集索引通常提供更快的数据访问速度。聚集索引和非聚集索引的区别，如字典默认按字母顺序排序，读者如知道某个字的读音可根据字母顺序快速定位。因此聚集索引和表的内容是在一起的。如读者需查询某个生僻字，则需按字典前面的索引，举例按偏旁进行定位，找到该字对应的页数，再打开对应页数找到该字。这种通过两个地方而查询到某个字的方式就如非聚集索引。

&nbsp; 

---

&nbsp; 

## Reference
Name|Link|Remarks
:---:|:---:|:---:
《SQL必知必会》|Null|Null