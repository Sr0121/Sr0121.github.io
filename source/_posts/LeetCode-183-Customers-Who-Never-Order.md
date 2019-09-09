---
title: 'LeetCode:183. Customers Who Never Order'
date: 2019-08-22 15:50:06
categories: LeetCode
tags:
  - LeetCode
  - SQL
---

**题目描述**

Suppose that a website contains two tables, the `Customers` table and the `Orders` table. Write a SQL query to find all customers who never order anything.

Table: `Customers`.

```
+----+-------+
| Id | Name  |
+----+-------+
| 1  | Joe   |
| 2  | Henry |
| 3  | Sam   |
| 4  | Max   |
+----+-------+
```

Table: `Orders`.

```
+----+------------+
| Id | CustomerId |
+----+------------+
| 1  | 3          |
| 2  | 1          |
+----+------------+
```

Using the above tables as example, return the following:

```
+-----------+
| Customers |
+-----------+
| Henry     |
| Max       |
+-----------+
```

<!--more-->



这题考查的是sql中in的用法，找到customers中不在orders的那些id就可以了

```sql
select name as Customers
from customers
where id not in (select customerid from orders);
```

