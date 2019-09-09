---
title: 'LeetCode:176. Second Highest Salary'
date: 2019-08-19 11:17:19
categories: LeetCode
tags: 
 - LeetCode
 - SQL
---

**题目描述**

Write a SQL query to get the second highest salary from the `Employee` table.

```
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```

For example, given the above Employee table, the query should return `200` as the second highest salary. If there is no second highest salary, then the query should return `null`.

```
+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+
```

<!--more-->

查找第二大的元素，只需要在where语句中过滤掉最大的元素后再使用max即可

**代码实现**

```sql
select max(Salary) as SecondHighestSalary from Employee where Salary < (select max(Salary) from Employee)
```

