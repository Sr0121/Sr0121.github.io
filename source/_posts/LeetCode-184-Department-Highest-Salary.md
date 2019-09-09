---
title: 'LeetCode:184. Department Highest Salary'
date: 2019-08-22 16:11:12
categories: LeetCode
tags:
  - LeetCode
  - SQL
---

**题目描述**

The `Employee` table holds all employees. Every employee has an Id, a salary, and there is also a column for the department Id.

```
+----+-------+--------+--------------+
| Id | Name  | Salary | DepartmentId |
+----+-------+--------+--------------+
| 1  | Joe   | 70000  | 1            |
| 2  | Jim   | 90000  | 1            |
| 3  | Henry | 80000  | 2            |
| 4  | Sam   | 60000  | 2            |
| 5  | Max   | 90000  | 1            |
+----+-------+--------+--------------+
```

The `Department` table holds all departments of the company.

```
+----+----------+
| Id | Name     |
+----+----------+
| 1  | IT       |
| 2  | Sales    |
+----+----------+
```

Write a SQL query to find employees who have the highest salary in each of the departments. For the above tables, your SQL query should return the following rows (order of rows does not matter).

```
+------------+----------+--------+
| Department | Employee | Salary |
+------------+----------+--------+
| IT         | Max      | 90000  |
| IT         | Jim      | 90000  |
| Sales      | Henry    | 80000  |
+------------+----------+--------+
```

**Explanation:**

Max and Jim both have the highest salary in the IT department and Henry has the highest salary in the Sales department.

<!--more-->



首先需要把两张表根据departmentid join起来，接着需要在employee表中找到每个department中salary的最高值，并且记录其对应的departmentid，最后在join起来的最终结果中寻找每个(departmentid, 最高的salary)所对应的组。

**代码实现**

```sql
select department.name as Department, employee.name as Employee, Salary
from employee
join department
on employee.departmentid = department.id
where (employee.departmentid, Salary) in (
    select departmentid, max(salary)
    from employee
    group by departmentid
);
```

