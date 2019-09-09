---
title: 'LeetCode:177. Nth Highest Salary'
date: 2019-08-19 11:52:49
categories: LeetCode
tags:
 - LeetCode
 - SQL
---

**题目描述**

Write a SQL query to get the *n*th highest salary from the `Employee` table.

```
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```

For example, given the above Employee table, the *n*th highest salary where *n* = 2 is `200`. If there is no *n*th highest salary, then the query should return `null`.

```
+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| 200                    |
+------------------------+
```

<!--more-->

这里需要使用函数实现查询第N大的salary，考察的是对limit的使用。

limit n, m表示除去前n项后，再输出m项，因此在这里需要limit N-1, 1就可以满足要求。但是由于limit语句中不能做算术操作，因此要将N-1赋值给另外一个变量后M后，再使用limit M, 1。

赋值的时候注意SQL是大小写不敏感的。

**代码实现**

```sql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
declare M int;
set M = N-1;
  RETURN (
      # Write your MySQL query statement below.
      select distinct Salary from Employee order by Salary desc limit M, 1
  );
END
```

