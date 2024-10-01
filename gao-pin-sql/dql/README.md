# DQL

## 计算字符串中字符数

计算字符串中字符数的最佳函数是 <mark style="color:blue;">**CHAR\_LENGTH**</mark>**(str)**，它返回字符串 str 的长度。

另一个常用的函数 LENGTH(str) 只能计算只包含英文字符，没有特殊字符的，否则，LENGTH() 可能会返回不同的结果，因为该函数返回字符串 str 的字节数，某些字符包含多于 1 个字节。

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
