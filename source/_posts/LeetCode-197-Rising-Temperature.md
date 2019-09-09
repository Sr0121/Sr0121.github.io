---
title: 'LeetCode:197. Rising Temperature'
date: 2019-08-29 14:42:01
categories: LeetCode
tags:
  - LeetCode
  - SQL
---

**题目描述**

Given a `Weather` table, write a SQL query to find all dates' Ids with higher temperature compared to its previous (yesterday's) dates.

```
+---------+------------------+------------------+
| Id(INT) | RecordDate(DATE) | Temperature(INT) |
+---------+------------------+------------------+
|       1 |       2015-01-01 |               10 |
|       2 |       2015-01-02 |               25 |
|       3 |       2015-01-03 |               20 |
|       4 |       2015-01-04 |               30 |
+---------+------------------+------------------+
```

For example, return the following Ids for the above `Weather` table:

```
+----+
| Id |
+----+
|  2 |
|  4 |
+----+
```

<!--more-->



考查date_sub的用法，date_sub(date, interval k day)为找到date的前k天并返回。

date可用curdate()表示今天。

**代码实现**

```
select s.id from weather as s, weather as t
where s.temperature > t.temperature and t.recorddate = date_sub(s.recorddate, interval 1 day);
```

