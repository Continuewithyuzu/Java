# DQL

## 计算字符串中字符数

计算字符串中字符数的最佳函数是 <mark style="color:blue;">**CHAR\_LENGTH**</mark>**(str)**，它返回字符串 str 的长度。

另一个常用的函数 LENGTH(str) 只能计算只包含英文字符，没有特殊字符的，否则，LENGTH() 可能会返回不同的结果，因为该函数返回字符串 str 的字节数，某些字符包含多于 1 个字节。

***

## join 链接类型

* INNER JOIN ：内连接, 可以只写JOIN ,<mark style="color:blue;">**只有连接的两个表中，都存在连接标准的数据才会保留下来，相当于两个表的交集**</mark>。如果前后连接的是同一个表，也叫自连接。
* LEFT JOIN ：左连接，也叫左外连接。操作符左边表中符合WHERE子句中的所有记录将会被返回，操作右边表中如果没有符合ON后面连接的条件时，那么右边表指定选择的列将会返回NULL。
* RIGHT JOIN：右连接，也叫右外连接。返回右边表所有符合WHERE语句的记录，左表中匹配不上的字段值用NULL来代替。
* &#x20;FULL JOIN：全连接。返回所有表中符合WHERE语句条件的所有记录。
* **USING 关键字**
  * 当JOIN…ON后面作为合并条件的列名时，在两个表中相同时，可以使用USING\
    (…,…)来简化，取代ON…AND…
  * 如果列名不一样，是不能够使用USING 关键字来简化的，需要特别注意

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

***

## 外连接查询

外连接查询分为<mark style="color:blue;">左外连接查询</mark>和<mark style="color:blue;">右外连接查询</mark>

### 语法：

```sql
--左外连接
select 字段1,字段2..
from 表1 left (outer) join 表2 on 过滤条件;
--右外连接
select 字段1,字段2..
from 表1 right (outer) join 表2 on 过滤条件;
```

### 例子：1378、使用唯一标识码替换员工ID

```sql
SELECT 
    Employees.name,EmployeeUNI.unique_id
FROM
    Employees
left join
    EmployeeUNI
on
    EmployeeUNI.id=Employees.id
```

### 区别如下

左外连接：是表1和表2的交集再并上表1的其他数据

右外连接：是表1和表2的交集再并上表2的其他数据

***

## 内连接查询

语法：

```sql
select <字段名>
from <表a>
JOIN <表b>
ON a.<字段名> = b.<字段名>;
```

例子：[1068](1068.-chan-pin-xiao-shou-fen-xi.md)

***

## 模糊查询（like）

```
_:单个任意字符
%:多个任意个字符
```

```sql
--查询users表中姓名第一个字为李的记录
select *from users where name like '李%';
--查询users表中姓名第二个字为李的记录
select *from users where name like '_李%';
--查询users表中姓名含有李字的记录
select *from users where name like '%李%';
--查询users表中姓名是两个字的记录
select *from users where name like '__';
```

***

## 排序

默认升序：esc

降序：desc

***

## 分页查询（limit）：

<mark style="color:blue;">**第一条记录的索引是0**</mark>

```sql
--查询users表中的前10行条记录
select *from users limit 10;
--查询users表中第2~11条记录 (从第2条记录开始累加10条记录)
select *from users limit 1,10;
--查询users表中第5~17条记录 (从第5条记录开始累加13条记录)
select *from users limit 4,13;
```

***

## `case-when-then-else-end`语法

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

例题：[1661、](1661-mei-tai-ji-qi-de-jin-cheng-ping-jun-yun-xing-shi-jian.md)
