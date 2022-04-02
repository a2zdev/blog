---
layout: default 
title: oracle常用sql
---

### oracle常用sql

1、检索数据库中包文本包含某个具体的文本

``` sql
select * from all_source where TEXT like '%aaaa%'
```
2、检索表中包含触发器
``` sql
select * from user_triggers where table_owner = 'xxx' and table_name = upper('table_name');
```
3、检索表锁
以下几个为相关表
```sql
SELECT * FROM v$lock;
SELECT * FROM v$sqlarea;
SELECT * FROM v$session;
SELECT * FROM v$process ;
SELECT * FROM v$locked_object;
SELECT * FROM all_objects;
SELECT * FROM v$session_wait;
```

3.1 查看被锁的表
```sql
select b.owner,b.object_name,a.session_id,a.locked_mode from v$locked_object a,dba_objects b where b.object_id = a.object_id;
```
3.2 查看那个用户那个进程照成死锁
```sql
select b.username,b.sid,b.serial#,logon_time from v$locked_object a,v$session b where a.session_id = b.sid order by b.logon_time;
```
3.3 查看连接的进程
```sql
SELECT sid, serial#, username, osuser FROM v$session;
```
3.4 查出锁定表的sid, serial#,os_user_name, machine_name, terminal，锁的type,mode
```sql
SELECT s.sid, s.serial#, s.username, s.schemaname, s.osuser, s.process, s.machine,
s.terminal, s.logon_time, l.type
FROM v$session s, v$lock l
WHERE s.sid = l.sid
AND s.username IS NOT NULL
ORDER BY sid;
```
这个语句将查找到数据库中所有的DML语句产生的锁，还可以发现，
任何DML语句其实产生了两个锁，一个是表锁，一个是行锁。

3.5 杀掉进程 sid,serial#
```sql
alter system kill session'210,11562';
```
