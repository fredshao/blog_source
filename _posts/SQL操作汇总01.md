---
title: SQL操作汇总01
date: 2018-04-23 21:59:01
tags: 机器学习
---

```sql
/*分行显示，比较清晰，关键字大写，其他字段小写*/

SELECT *
FROM orders;

SELECT id, account_id, occurred_at
FROM orders;

SELECT occurred_at, account_id, channel 
FROM web_events 
LIMIT 15;

/*SQL默认是以升序排列的，加上DESC就是以降序*/
SELECT id, account_id, total_amt_usd 
FROM orders 
ORDER BY total_amt_usd DESC 
LIMIT 5;

SELECT *
FROM orders
WHERE gloss_amt_usd >= 1000
LIMIT 5;

SELECT name, website, primary_poc
FROM accounts
WHERE name = 'Exxon Mobil';

/*派生列*/
SELECT id, account_id, standard_amt_usd / standard_qty AS new_column
FROM orders
LIMIT 10;

/*选择出所有name为开头为C的列*/
SELECT *
FROM accounts
WHERE name LIKE 'C%';

/*name中包含'one'的列*/
SELECT name
FROM accounts
WHERE name LIKE '%one%';

/*name以's'结尾的列*/
SELECT name
FROM accounts
WHERE name LIKE '%s';

/*name为'Walmart'或'Target'或'Nordstrom'的列*/
SELECT name, primary_poc, sales_rep_id
FROM accounts
WHERE name IN('Walmart','Target','Nordstrom');

SELECT name, primary_poc, sales_rep_id
FROM accounts
WHERE name NOT IN('Walmart','Target','Nordstrom');

SELECT *
FROM web_events
WHERE channel NOT IN ('organic','adwords');

SELECT *
FROM orders
WHERE standard_qty > 1000 AND poster_qty = 0 AND gloss_qty = 0;

SELECT *
FROM accounts
WHERE name NOT LIKE 'C%' AND name LIKE '%s';

SELECT *
FROM web_events
WHERE channel IN ('organic','adwords') 
			AND occurred_at >= '2016-1-1' AND occurred_at <= '2016-12-31'
ORDER BY occurred_at DESC;

/*在日期中使用 BETWEEN 很麻烦，虽然 BETWEEN 一般情况下不包括端点值，假设时间是 00:00:00（即午夜），这就是我们将右边的时间点设置为 '2017-01-01' 的原因了.*/
SELECT *
FROM web_events
WHERE channel IN ('organic', 'adwords') 
			AND occurred_at BETWEEN '2016-01-01' AND '2017-01-01'
ORDER BY occurred_at DESC;

SELECT *
FROM orders
WHERE standard_qty = 0 AND (gloss_qty > 1000 OR poster_qty > 1000);

/*查找以 'C' 或 'W' 开头的所有公司名 (company names)，主要联系人 (primary contact) 包含 'ana' 或 'Ana'，但不包含 'eana'。*/
SELECT *
FROM accounts
WHERE (name LIKE 'C%' OR name LIKE 'W%') 
           AND ((primary_poc LIKE '%ana%' OR primary_poc LIKE '%Ana%') 
           AND primary_poc NOT LIKE '%eana%');
```

