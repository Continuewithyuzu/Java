# 1581、进店却未交易的顾客

其实题目不难，难在了读题上

其实就真的左连接，然后找出null就行了

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

sql：

```sql
SELECT customer_id, count(customer_id) count_no_trans
FROM Visits v
LEFT JOIN transactions t 
ON v.visit_id = t.visit_id
WHERE transaction_id IS NULL
GROUP BY customer_id;
```

题目比较具有迷惑性
