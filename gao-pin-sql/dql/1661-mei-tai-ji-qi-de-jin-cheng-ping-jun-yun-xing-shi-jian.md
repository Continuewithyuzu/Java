# 1661、每台机器的进程平均运行时间

## 构造法：不用自连接的方法

主要的思路比较有意思，不是用了题目想让用的自连接而是通过一个比较巧妙的方法计算每个机器的时间和然后取平均值，具体的重点是`case-when-then-else-end`语法

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt="" width="563"><figcaption></figcaption></figure>

```sql
SELECT 
    machine_id, 
    ROUND(SUM(CASE WHEN activity_type = 'end' THEN timestamp ELSE -timestamp END) / 
count(distinct process_id), 3) AS processing_time
FROM activity
GROUP BY machine_id
```

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## 自连接方法：

```sql
select 
a1.machine_id,
round(avg(a2.timestamp -a1.timestamp ),3) as processing_time 
from  Activity as a1 join Activity as a2 on 
a1.machine_id=a2.machine_id and 
a1.process_id=a2.process_id and 
a1.activity_type ='start' and 
a2.activity_type ='end' 
group by machine_id;
```

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>
