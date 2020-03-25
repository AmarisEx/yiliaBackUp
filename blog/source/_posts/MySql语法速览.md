---
title:  MySql语法速览
date: 2020-03-23 21:58:00
tags:
	- Mysql
---

# 登录数据库

```sql
  mysql -u root
```
<!--more-->
# 查询数据库

```sql
  show databases;
```

# 选中数据库

```sql
  use sys
```

# 查询该数据库（查）

```sql
  select * from course;
```

```sql
  select * from course where id=1;
```

# 退出数据库

```sql
 exit;
```

# 创建新的数据库

```sql
  create database mycourse;
```

# 查看表

```sql
  show tables;
```

# 创建及删除数据表

```sql
CREATE TABLE course(
     name VARCHAR(20),
  teacher VARCHAR(20));
```

```sql
drop table course;
```

# 查看表结构

```sql
 describe course;
```

# 插入新字段

```sql
   alter table course add id int;
```

# 插入记录（增）

```sql
   mysql> INSERT INTO course
        values("DataMining","Shao",1);
```

# 更新记录（改）

```sql
 update course set teacher="Hu" where id=3;
```

# 删除记录（删）

```sql
 delete from course where teacher="Hu";
```

# LIKE子句

- 如果没有使用百分号 %, LIKE 子句与等号 = 的效果是一样的。  

```sql
 select * from course where teacher like "%ao";
```

```sql
   +------------+---------+------+
   | name       | teacher | id   |
   +------------+---------+------+
   | DataMining | Shao    |    1 |
   | Runing     | Hao     |    3 |
   +------------+---------+------+
```



# 主键约束primary key
- 主键可以唯一确定一条数据，字段值不可重复
- 创建主键在 类型后＋`primary key`
- 修改为主键

```sql
alter table course modify id int primary key;
```

```sql
mysql> desc course;
+-------------+--------------+------+-----+---------+-------+
| Field       | Type         | Null | Key | Default | Extra |
+-------------+--------------+------+-----+---------+-------+
| id          | int(11)      | NO   | PRI | NULL    |       |
| courseTitle | varchar(255) | YES  |     | NULL    |       |
| teacher     | varchar(255) | YES  |     | NULL    |       |
| timeTable   | varchar(0)   | YES  |     | NULL    |       |
+-------------+--------------+------+-----+---------+-------+
4 rows in set (0.05 sec)

mysql> alter table course drop primary key;


mysql> alter table course add primary key(id);
```

# 联合主键
- 且的关系，两个主键都相同的数据不行
- 有一个相同可以

```sql
mysql> create table student2(
    -> id int(10),
    -> name varchar(20),
    -> password varchar(20),
    -> primary key(id,name));
```


# 自增约束
- 结合主键使用，可以自动赋值
```sql

mysql> insert into student2
    -> values(NULL,"mari");
Query OK, 1 row affected (0.00 sec)

mysql> select * from student2;
+----+------+
| id | name |
+----+------+
|  1 | mari |
+----+------+
1 row in set (0.04 sec)
```
# 唯一约束
- 字段值唯一（与Primary key区别：unique 可为空，最多一处空）

```sql
mysql> alter table student3 add unique(name);
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc student3;

+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(20)     | YES  |     | NULL    |       |
| name  | varchar(20) | YES  | UNI | NULL    |       |
+-------+-------------+------+-----+---------+-------+
mysql> alter table student3 drop index name;//删除unique约束
```
# 非空约束
- 修饰的字段不可为空

```sql

mysql> create table stu4(
    -> id int(20),
    -> name varchar(20) not null
    -> );
```
# 默认约束
- 插入字段值时，没有传值就会使用默认值
# 外键约束
- 链接它表的键
```sql
mysql> alter table student add foreign key(class_id) references course(id);
mysql> desc student;
+----------+--------------+------+-----+---------+-------+
| Field    | Type         | Null | Key | Default | Extra |
+----------+--------------+------+-----+---------+-------+
| id       | int(11)      | NO   | PRI | NULL    |       |
| name     | varchar(255) | YES  |     | NULL    |       |
| number   | varchar(0)   | YES  |     | NULL    |       |
| class_id | int(11)      | YES  | MUL | NULL    |       |
+----------+--------------+------+-----+---------+-------+
```

