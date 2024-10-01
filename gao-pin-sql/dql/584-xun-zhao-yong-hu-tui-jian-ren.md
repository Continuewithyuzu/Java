# 584、寻找用户推荐人

也是最基本的DQL，**查询不为NULL值(is not null),为NULL值(is null)**

```sql
SELECT name FROM Customer WHERE referee_id != 2 OR referee_id IS null
```
