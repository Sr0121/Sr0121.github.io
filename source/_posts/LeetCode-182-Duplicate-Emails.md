---
title: 'LeetCode:182. Duplicate Emails'
date: 2019-08-22 15:44:28
categories: LeetCode
tags:
  - LeetCode
  - SQL
---

**题目描述**

Write a SQL query to find all duplicate emails in a table named `Person`.

```
+----+---------+
| Id | Email   |
+----+---------+
| 1  | a@b.com |
| 2  | c@d.com |
| 3  | a@b.com |
+----+---------+
```

For example, your query should return the following for the above table:

```
+---------+
| Email   |
+---------+
| a@b.com |
+---------+
```

<!--more-->

这题考查having语句的用法

**代码实现**

```sql
select email 
from person 
group by email
having count(email) > 1;
```

