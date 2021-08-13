---
title: Database_Leetcode
author: "Misty"
tags: ["Database"]
categories: ["Coding"]
date: 2021-06-12
---


## 175. 组合两个表

#### 题目
* https://leetcode-cn.com/problems/combine-two-tables/
* right join

#### 解答

```sql
select FirstName, LastName, City, State
from address
right join person
on person.personId = address.personId
```


## 176. 第二高的薪水

#### 题目
* https://leetcode-cn.com/problems/second-highest-salary/
* ifnull(a,b)
* limit 1 offset 1
* distinct

#### 解答

```sql
select ifnull((select distinct Salary from employee order by salary desc LIMIT 1 OFFSET 1),null) as SecondHighestSalary
```


## 178. 分数排名

#### 题目
* https://leetcode-cn.com/problems/rank-scores/
* [窗口函数](https://zhuanlan.zhihu.com/p/138282683)
* rank()/dense_rank()/row_number()

#### 解答

```sql
select Score, dense_rank() over (order by Score desc ) as 'Rank'
from Scores
```


## 181. 超过经理收入的员工

#### 题目
* https://leetcode-cn.com/problems/employees-earning-more-than-their-managers/
* 自连接/笛卡尔积

#### 解答

```sql
select a.name as 'Employee'
from employee a
inner join employee b
on a.Managerid = b.id
where a.Salary > b.Salary
```


## 184. 部门工资最高的员工

#### 题目
* https://leetcode-cn.com/problems/department-highest-salary/
* 窗口函数/也可以用in

#### 解答

```sql
select Department, Employee, Salary
from (
    select 
    a.Id, 
    a.Name as 'Employee', 
    a.Salary as 'Salary', 
    b.Name as 'Department', 
    rank() over (Partition by b.name order by a.Salary desc) as ranking
    from Employee a
    inner join Department b
    on a.DepartmentId = b.Id) c
where ranking = 1
```

```sql
SELECT
	Department.NAME AS Department,
	Employee.NAME AS Employee,
	Salary 
FROM
	Employee,
	Department 
WHERE
	Employee.DepartmentId = Department.Id 
	AND ( Employee.DepartmentId, Salary ) 
    IN (SELECT DepartmentId, max( Salary ) 
        FROM Employee 
        GROUP BY DepartmentId )
```


## 185.部门工资前三高的所有员工  

#### 题目
* https://leetcode-cn.com/problems/department-top-three-salaries/
* 窗口函数

#### 解答

```sql
select Department, Employee, Salary
from(
    select 
    a.Id, 
    a.Name as 'Employee', 
    a.Salary as 'Salary', 
    b.Name as 'Department', 
    dense_rank() over (Partition by b.name order by a.Salary desc) as ranking
    from Employee a
    inner join Department b
    on a.DepartmentId = b.Id ) c
where ranking < 4
```


## 182.查找重复的电子邮箱  

#### 题目
* https://leetcode-cn.com/problems/duplicate-emails/
* count()

#### 解答

```sql
select distinct Email
from person
group by email
having count(email) >1
```


## 183.从不订购的客户  

#### 题目
* https://leetcode-cn.com/problems/customers-who-never-order/
* not in

#### 解答

```sql
select Name as 'Customers'
from customers
where id not in
(select a.id
from customers a
inner join Orders b
on a.id = b.CustomerId)
```


## 197.上升的温度 

#### 题目
* https://leetcode-cn.com/problems/rising-temperature/
* datediff(day1,day2)

#### 解答

```sql
select b.id
from Weather a
inner join Weather b
where datediff(b.recordDate,a.recordDate) = 1 and a.Temperature < b.Temperature
```


## 180. 连续出现的数字

#### 题目
* https://leetcode-cn.com/problems/consecutive-numbers/
* 连接表

#### 解答

```sql
select distinct 
    a.Num as 'ConsecutiveNums'
from 
    logs a, 
    logs b, 
    logs c
where 
    a.id = b.id + 1 
    and b.id = c.id + 1 
    and a.Num = b.Num 
    and b.Num = c.Num
```


## 177. 第N高的薪水

#### 题目
* https://leetcode-cn.com/problems/nth-highest-salary/
* ifnull(a,b)/distinct

#### 解答

```sql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  RETURN (
      # Write your MySQL query statement below.
      select 
      ifnull(
          (select distinct 
                Salary as 'getNthHighestSalary' 
            from 
                (select Salary, dense_rank() over (order by Salary desc) as 'ranking' from employee) a 
            where ranking = N)
      ,null)
  );
END
```


## 1777. 每家商店的产品价格

#### 题目
* https://leetcode-cn.com/problems/products-price-for-each-store/
* 行转列/group by聚合

#### 解答

```sql
select product_id,
        max(case when store = 'store1' then price else null end) as 'store1',
        max(case when store = 'store2' then price else null end) as 'store2',
        max(case when store = 'store3' then price else null end) as 'store3'
from Products
group by product_id
```

## 196. 删除重复的电子邮箱

#### 题目
* https://leetcode-cn.com/problems/delete-duplicate-emails/
* delete

#### 解答

```sql
delete a
from person a, person b
where a.Email = b.Email and a.id > b.id
```


## 262. 行程和用户

#### 题目
* https://leetcode-cn.com/problems/trips-and-users/
* 困难题，两次连接，统计取消率

#### 解答

```sql
select 
    T.Request_at as Day,
    round(sum(if(Status='completed',0,1))/count(T.Request_at),2) as 'Cancellation Rate'

from (
select Id, Client_Id, Driver_Id, City_Id, Status, Request_at from Trips
left join Users a on a.Users_Id = Client_id and a.Role = 'Client' 
left join Users b on b.Users_Id = Driver_id and b.Role = 'Driver' 
where a.Banned = 'No' and b.Banned = 'No'
) T

group by T.Request_at
having T.Request_at between '2013-10-01' and '2013-10-03'
```


## 601. 体育馆的人流量

#### 题目
* https://leetcode-cn.com/problems/human-traffic-of-stadium/
* 多表连接

#### 解答

```sql
select distinct
    a.*
from 
    (select * from Stadium where people >= 100) a,
    (select * from Stadium where people >= 100) b,
    (select * from Stadium where people >= 100) c
where 
    (a.id = b.id - 1 and b.id = c.id - 1) 
    or (a.id = b.id + 1 and b.id = c.id  + 1) 
    or (a.id = b.id + 1 and b.id = c.id  - 2)    
order by 
    a.id 
```


## 1179. 重新格式化部门表

#### 题目
* https://leetcode-cn.com/problems/reformat-department-table/
* case when

#### 解答

```sql
select 
    id,
    max(case when month = 'Jan' then revenue else null end) as 'Jan_Revenue',
    max(case when month = 'Feb' then revenue else null end) as 'Feb_Revenue',
    max(case when month = 'Mar' then revenue else null end) as 'Mar_Revenue',
    max(case when month = 'Apr' then revenue else null end) as 'Apr_Revenue',
    max(case when month = 'May' then revenue else null end) as 'May_Revenue',
    max(case when month = 'Jun' then revenue else null end) as 'Jun_Revenue',
    max(case when month = 'Jul' then revenue else null end) as 'Jul_Revenue',
    max(case when month = 'Aug' then revenue else null end) as 'Aug_Revenue',
    max(case when month = 'Sep' then revenue else null end) as 'Sep_Revenue',
    max(case when month = 'Oct' then revenue else null end) as 'Oct_Revenue',
    max(case when month = 'Nov' then revenue else null end) as 'Nov_Revenue',
    max(case when month = 'Dec' then revenue else null end) as 'Dec_Revenue'
from 
    Department
group by 
    id
```


## 626. 换座位

#### 题目
* https://leetcode-cn.com/problems/exchange-seats/
* case when

#### 解答

```sql
SELECT
    (CASE
        WHEN MOD(id, 2) != 0 AND counts != id THEN id + 1
        WHEN MOD(id, 2) != 0 AND counts = id THEN id
        ELSE id - 1
    END) AS id,
    student
FROM
    seat,
    (SELECT
        COUNT(*) AS counts
    FROM
        seat) AS seat_counts
ORDER BY id ASC;
```

