---
title: mysql note
date: 2019-09-10 15:01:08
tags: mysql
---
### 备份全部数据库
```bash
mysqldump -uroot -p --all-databases > sqlfile.sql
source d:\sqlfile.sql;	// 导入
```

### 删除table的主键字段，重新添加主键，让自增id重新排序
```sql
alter table dk_wbacategory drop column cate_id;
alter table dk_wbacategory add cate_id int(10) not null primary key auto_increment first;
```

### 复制记录
```sql
insert into dk_wbarticle select * from dk_wbarticle where id=55
```

### explain语句，分析查询结果
```bash
explain + select 语句

+----+-------------+-----------+-------+---------------+---------+---------+-------+
| id | select_type | table | type | possible_keys | key | key_len | ref | rows | Extra |
+----+-------------+-----------+-------+---------------+---------+---------+-------+
| 1 | SIMPLE | ecs_goods | const | PRIMARY | PRIMARY | 3 | const | 1 | |
+----+-------------+-----------+-------+---------------+---------+---------+-------+
1 row in set (0.02 sec)

- select_type：select查询的类型，主要是区别普通查询和联合查询、子查询之类的复杂查询。
- type：type显示的是访问类型，是较为重要的一个指标，结果值从好到坏依次是：system > const > eq_ref > ref > fulltext > ref_or_null > index_merge > unique_subquery > index_subquery > range > index > ALL
一般来说，得保证查询至少达到range级别，最好能达到ref。
- possible_keys：指出MySQL能使用哪个索引在该表中找到行。如果是空的，没有相关的索引。这时要提高性能，可通过检验WHERE子句，看是否引用某些字段，或者检查字段不是适合索引。
- key：显示MySQL实际决定使用的键。如果没有索引被选择，键是NULL。
- key_len：显示MySQL决定使用的键长度。如果键是NULL，长度就是NULL。文档提示特别注意这个值可以得出一个多重主键里mysql实际使用了哪一部分。
- ref：显示哪个字段或常数与key一起被使用。
- Extra：如果是Only index，这意味着信息只用索引树中的信息检索出的，这比扫描整个表要快。
如果是where used，就是使用上了where限制。
如果是impossible where 表示用不着where，一般就是没查出来啥。
如果此信息显示Using filesort或者Using temporary的话会很吃力，WHERE和ORDER BY的索引经常无法兼顾，如果按照WHERE来确定索引，那么在ORDER BY时，就必然会引起Using filesort，这就要看是先过滤再排序划算，还是先排序再过滤划算.
```

### 分析mysql语句性能
```sql
set profiling=1;	// 开启功能
select * from table; 
show profiles; 		
show profile for query n;     // n对应SHOW PROFILES输出中的Query_ID
```

### 查看数据库大小
```sql
select concat((sum(data_length)+sum(index_length))/1024/1024,'m') from information_schema.tables where table_schema='数据库名';
```

### 查看数据库各个表的大小
```sql
select table_name,concat((data_length+index_length)/1024/1024,'m') daxiao,table_rows as rows from information_schema.tables where table_schema='数据库名' order by daxiao desc,rows desc;
```

### 批量修改数据表前缀
```sql
SELECT CONCAT('ALTER TABLE ',table_name,' RENAME TO pt_',substring(table_name, 4),';') FROM information_schema. TABLES WHERE table_name LIKE 'li%';
```

### mysql search duplicate rows
```sql
SELECT email, COUNT(email) FROM contacts GROUP BY email HAVING COUNT(email) > 1;


```

### mysql delete duplicate rows
```sql
DELETE t1 FROM contacts t1 INNER JOIN contacts t2 WHERE t1.id < t2.id AND t1.email = t2.email;
```