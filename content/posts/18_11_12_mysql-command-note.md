---
title: "［MySQL］SQL語法筆記"
date: 2018-11-12T11:02:53+08:00
draft: false
categories: [Web Back-end Development]
tags: [MySQL]
---

## 基本資料庫操作

* 通常這些行為在介面化工具輔助下，較不會使用語法去操作了。

### 建立/刪除/使用資料庫(database)

```sql
# [db_name]為自定資料庫名稱
# 建立資料庫
create database [db_name];
# 刪除資料庫
drop database [db_name];
# 使用資料庫
use [db_name];
```

### 列出所有資料庫

```sql
show databases;
```

### 建立/刪除資料表(table)

```sql
# [table_name]為自定資料表名稱；[column]為自定欄位名稱；[data_type]為設定資料型態
# 建立資料表
create table [table_name] (
	[column1] [data_type],
	[column2] [data_type],
	[column3] [data_type],
	...
);
# 刪除資料表
drop table [table_name];
```

`Tips`

創建資料表時常用的資料型態(data type)：

資料型態 | 範圍 | 說明
-------|-------|-------
INT(size) | 有符號範圍：(-2147483648，2147483647)；無符號範圍：(0，4294967295) | 大整數值
CHAR(size) | 0~255字元 | 固定長度字串
VARCHAR(size) | 0~255字元 | 不固定長度字串
TEXT | 0~65535字元 | 不固定長度字串
DATE | 1000-01-01 ~ 9999-12-31 | 日期，格式：YYYY-MM-DD
DATETIME | 1000-01-01 00:00:00 ~ 9999-12-31 23:59:59 | 日期與時間，格式：YYYY-MM-DD HH:MI:SS
TIME | -838:59:59 ~ 838:59:59 | 時間，格式：HH:MI:SS

* 更多型態：https://www.w3schools.com/sql/sql_datatypes.asp

`Example`

```sql
# auto_increment表示會自動累加數值；primary key為主鍵設定
create table student (
	id int(10) auto_increment primary key,
	name varchar(20),
	home varchar(20)
);
```

### 修改/新增/刪除資料表欄位

```sql
# 修改資料表欄位
alter table [table_name] change column [old_column_name] [new_column_name] [new_data_type];
# 新增資料表欄位
alter table [table_name] add column [column_name] [data_type];
# 刪除資料表欄位
alter table [table_name] drop column [column_name];
```

`Example`

```sql
alter table student add column gender varchar(10);
```

### 列出資料表欄位資訊

```sql
describe [table_name];
```

### 清空資料表內容

* 只清除資料內容，不刪除結構，auto_increment會從1開始。

```sql
truncate table [table_name];
```

## 常用資料庫語法(插入、更新、查詢等)

### 插入欄位新資料(insert)

```sql
# [table_name]為自定資料表名稱；[column]為欄位名稱；[value]為欲插入的值
insert into [table_name] ([column1], [column2], [column3], ...) values ([value1], [value2], [value3], ...);
```

`Example`

```sql
insert into student (id, name, home, gender) values (null, 'test', 'taipei', 'male');
```

`Tips`

* 已經設定auto_increment屬性的欄位，value直接設定`null`即可。
* 若是要設定時間(現在時間)，則在欄位value設定`NOW()`即可。

### 更新欄位資料內容(update)

```sql
# [table_name]為自定資料表名稱
# [column]為欄位名稱；[value]為修改後的值
# [condition]為自定條件式
update [table_name] set [column1] = [value1], [column2] = [value2], ... where [condition];
```

`Example`

```sql
update student set name='test2', home='taitung' where id = 2;
```

### 查詢欄位資料(select)

```sql
# [column]為欄位名稱；[table_name]為自定資料表名稱
# 查詢單一欄位資料
select [column] from [table_name];
# 查詢多個欄位資料
select [column1], [column2], ... from [table_name];
# 查詢所有欄位資料
select * from [table_name];
# 查詢該欄位「不重複」的值
select distinct [column] from [table_name];
```

`Example`

```sql
select name, home from student;
```

### 條件式查詢資料(where/not/and/or)

```sql
# [table_name]為自定資料表名稱；[condition]為自定條件式
# 條件式查詢(單一條件)
select * from [table_name] where [condition];
# 條件式查詢(單一條件 NOT)
select * from [table_name] where not [condition];
# 條件式查詢(多重條件 AND)
select * from [table_name] where [condition1] and [condition2];
# 條件式查詢(多重條件 OR)
select * from [table_name] where [condition1] or [condition2];
```

`Example`

```sql
select * from student where home='taichung' and gender='female';
```

`Tips`

* 通常在進行條件式查詢時，會查詢整個資料表`select *`。

### 單一欄位單一/多個資料查詢(in)

```sql
# [table_name]為自定資料表名稱
# [column]為欄位名稱；[value]為欄位內容值
# 單一欄位單一資料查詢
select * from [table_name] where [column] in ([value]);
# 上句就如同下句的意思
select * from [table_name] where [column] = [value];

# 單一欄位多個資料查詢
select * from [table_name] where [column] in ([value1], [value2], [value3], ...);
```

`Tips`

* `in`可以使用在subquery，通常有兩個資料表以上進行查詢時。

`Example`

```sql
select * from student where home in ('taipei', 'taichung');
```

### 查詢欄位資料是否為空值(is null)

```sql
# [table_name]為自定資料表名稱；[column]為欄位名稱
# 查詢欄位資料是空值
select * from [table_name] where [column] is null;
# 查詢欄位資料不是空值
select * from [table_name] where [column] is not null;
```

`Example`

```sql
select * from student where home is null;
```

### 查詢介於範圍值之間的欄位資料(between)

```sql
# [table_name]為自定資料表名稱
# [column]為欄位名稱；[value]為欄位內容值
select * from [table_name] where [column] between [value1] and [value2];
```

`Example`

```sql
select * from student where age between 20 and 30;
```

### 查詢結果遞增/遞減排序(order by)

* 預設為asc，如果沒有寫asc或desc，則結果會遞增排序顯示。

```sql
# [table_name]為自定資料表名稱；[column]為欄位名稱
# 查詢結果遞增排序
select * from [table_name] order by [column] asc;
# 查詢結果遞減排序
select * from [table_name] order by [column] desc;
```

`Example`

```sql
select * from student order by age desc;
```

### 查詢第幾筆範圍結果(limit)

```sql
# [table_name]為自定資料表名稱；[number]填入數目
# 例如：limit 3, 5 --> 則會顯示第四筆與第五筆
# 如果只填入一個數字，則會顯示前n筆資料
select * from [table_name] limit [number], [number];
```

`Example`

```sql
select * from student limit 3, 5;
```

### 查詢比對字串後結果(like)

```sql
# [table_name]為自定資料表名稱
# [column]為欄位名稱；['%string%']為比對字串內容
select * from [table_name] where [column] like ['%string%'];
```

`Example`

```sql
select * from student where name like '%test%';
```

`Tips`

各種字串比對寫法：

* '%a'：以a結尾的字串
* 'a%'：以a開頭的字串
* '%a%'：含有a的字串
* 'a%o'：以a開頭且以o結尾的字串
* '\_a\_'：字串只有三位且中間為a
* '\_a'：字串只有兩位且結尾為a
* 'a_'：字串只有兩位且開頭為a

### 查詢各種函式計算結果(AVG/COUNT/MAX/MIN/SUM)

```sql
# [column]為欄位名稱；[table_name]為自定資料表名稱；[condition]為自定條件式
# 找出該欄位的平均值
select AVG([column]) from [table_name] where [condition];
# 找出該欄位的筆數
select COUNT([column]) from [table_name] where [condition];
# 找出該欄位的最大值
select MAX([column]) from [table_name] where [condition];
# 找出該欄位的最小值
select MIN([column]) from [table_name] where [condition];
# 找出該欄位的計算總和
select SUM([column]) from [table_name] where [condition];
```

`Example`

```sql
select AVG(age) from student where home = 'taipei';
```

### 條件式刪除欄位資料(delete)

```sql
# [table_name]為自定資料表名稱；[condition]為自定條件式
# 刪除單一條件欄位資料
delete from [table_name] where [condition];
# 刪除多重條件欄位資料(AND)
delete from [table_name] where [condition1] and [condition2];
# 刪除多重條件欄位資料(OR)
delete from [table_name] where [condition1] or [condition2];
# 刪除資料表內所有資料，但auto_increment不會從1開始
delete from [table_name];
```

`Example`

```sql
delete from student where age = 30;
```

## 進階資料庫語法(合併、進階查詢等)

### Reference
---
* https://www.w3schools.com/sql/default.asp
* http://www.runoob.com/mysql/mysql-tutorial.html
* http://note.drx.tw/2012/12/mysql-syntax.html
* https://www.1keydata.com/tw/sql/sql.html
