# 1148、文章浏览Ⅰ

## 要点：

<mark style="color:blue;">**去重是**</mark><mark style="color:blue;">**`distinct`**</mark>

排序是`order by`

列重命名 `旧表名 AS 新表名`

```sql
SELECT distinct viewer_id AS id FROM Views WHERE author_id = viewer_id order by id
```
