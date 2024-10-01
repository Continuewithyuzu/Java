# 1378、使用唯一标识码替换员工ID

这里涉及到了[外连接查询](./#wai-lian-jie-cha-xun)中的左连接的知识点

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
