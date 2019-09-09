---
title: 'LeetCode:181. Employees Earning More Than Their Managers'
date: 2019-08-20 23:47:31
categories: LeetCode
tags:
  - LeetCode
  - SQL
---

**题目描述**

The `Employee` table holds all employees including their managers. Every employee has an Id, and there is also a column for the manager Id.

```
+----+-------+--------+-----------+
| Id | Name  | Salary | ManagerId |
+----+-------+--------+-----------+
| 1  | Joe   | 70000  | 3         |
| 2  | Henry | 80000  | 4         |
| 3  | Sam   | 60000  | NULL      |
| 4  | Max   | 90000  | NULL      |
+----+-------+--------+-----------+
```

Given the `Employee` table, write a SQL query that finds out employees who earn more than their managers. For the above table, Joe is the only employee who earns more than his manager.

```
+----------+
| Employee |
+----------+
| Joe      |
+----------+
```

<!--more-->

在where语句中查找出每行对应的manager的salary后进行比较即可。

**代码实现**

```
select s.name as Employee
from Employee as s
where s.Salary > (select t.Salary from Employee as t where t.id = s.managerid)
```

