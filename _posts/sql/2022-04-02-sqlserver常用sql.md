---
layout: default 
title: sqlserver常用sql
---

### sqlserver常用sql

1、检索数据库中包文本包含某个具体的文本

``` sql
select
    name,
    type_desc
from
    sys.all_sql_modules s
    inner join sys.all_objects o on s.object_id = o.object_id
where
    definition like '%aa%'
```

2、查询锁表
```sql
select *
from sys.dm_tran_locks
where resource_type = 'OBJECT';
```

3、查询死锁
```sql
select er.session_id,
       CAST(csql.text AS varchar(max)) AS CallingSQL
from master.sys.dm_exec_requests er WITH (NOLOCK)
         CROSS APPLY fn_get_sql(er.sql_handle) csql
where er.session_id in (select request_session_id from sys.dm_tran_locks where resource_type = 'OBJECT');
```