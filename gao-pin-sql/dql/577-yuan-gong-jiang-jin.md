# 577、员工奖金

这题用左连接，还是对连接的概念不够熟悉，不明白左连接和哟普连接的区别，哪个表连接到另一个表

我的代码：

```sql
SELECT name,bonus
FROM Employee
left join Bonus
on Employee.empId = Bonus.empId
WHERE bonus<1000 or bonus = null
```

犯了一个错误，判空写成了=null

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>
