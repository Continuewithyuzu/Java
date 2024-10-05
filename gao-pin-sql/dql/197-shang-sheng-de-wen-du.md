# 197、上升的温度

有自连接那味道了

代码：

<pre class="language-sql"><code class="lang-sql">SELECT 
    w1.id 
FROM 
<strong>    Weather w1,Weather w2 
</strong>WHERE 
    w1.recordDate = date_add(w2.recordDate, INTERVAL 1 DAY) 
AND 
    w1.Temperature>w2.Temperature
</code></pre>

值得注意的点：计算日期差的一个函数

```sql
w1.recordDate = date_add(w2.recordDate, INTERVAL 1 DAY) 
```
