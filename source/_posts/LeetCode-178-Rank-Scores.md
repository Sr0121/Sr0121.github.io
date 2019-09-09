---
title: 'LeetCode:178. Rank Scores'
date: 2019-08-19 22:57:12
categories: LeetCode
tags:
  - LeetCode
  - SQL
---

**题目描述**

Write a SQL query to rank scores. If there is a tie between two scores, both should have the same ranking. Note that after a tie, the next ranking number should be the next consecutive integer value. In other words, there should be no "holes" between ranks.

```
+----+-------+
| Id | Score |
+----+-------+
| 1  | 3.50  |
| 2  | 3.65  |
| 3  | 4.00  |
| 4  | 3.85  |
| 5  | 4.00  |
| 6  | 3.65  |
+----+-------+
```

For example, given the above `Scores` table, your query should generate the following report (order by highest score):

```
+-------+------+
| Score | Rank |
+-------+------+
| 4.00  | 1    |
| 4.00  | 1    |
| 3.85  | 2    |
| 3.65  | 3    |
| 3.65  | 3    |
| 3.50  | 4    |
+-------+------+
```

<!--more-->

这题的思路就是构建一张空的表格t，该表格中的score分数由原表格s生成，但是score唯一。

然后比较两张表格。对于每个s中的分数，需要统计t中比s的score更大或相等的数字有几个。

这里要注意的就是需要加上group by s.id的语句，这里的group by的功能大概就是为了在输出的时候，确定每个id都输出的意思。不加group by则只会输出一行。

**代码实现**

```sql
select s.Score, 
count(t.Score) as Rank
from Scores as s,
(select distinct Score from Scores) as t 
where s.Score <= t.score
group by s.id
order by s.Score desc;
```

