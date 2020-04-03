# SQL语法

[toc]

## 常用

```sql
-- 查看表信息
DESC bb;
```

## 简介

> - SQL，指结构化查询语言，全称是 Structured Query Language。
> - SQL 用来访问和处理数据库

> - SQL 面向数据库执行查询，取回数据，插入新的记录，更新数据，删除记录，创建新数据库，创建新表，创建存储过程，创建视图，设置表、存储过程和视图的权限

*一些最重要的 SQL 命令*

> - **SELECT** - 从数据库中提取数据
> - **UPDATE** - 更新数据库中的数据
> - **DELETE** - 从数据库中删除数据
> - **INSERT INTO** - 向数据库中插入新数据
> - **CREATE DATABASE** - 创建新数据库
> - **ALTER DATABASE** - 修改数据库
> - **CREATE TABLE** - 创建新表
> - **ALTER TABLE** - 变更（改变）数据库表
> - **DROP TABLE** - 删除表
> - **CREATE INDEX** - 创建索引（搜索键）
> - **DROP INDEX** - 删除索引

## 基础

### 创建

+ 建库

```mysql
CREATE DATABASE dbname;
```

+ 建表

```mysql
create table 学生
(学号 int NOT NULL primary key,
 姓名 varchar(10),
 性别 char(2) default '男',
 专业 char(20),
 系别 char(20),
 年级 char(20),
 班别 char(2),
 出生日期 date,
 地区来源 varchar(30),
 情况变动 char(10),
 政治面貌 char(8),
 民族  char(8) default'汉',
 总学分 int 
);
```

### SELECT 语句

> SELECT 语句用于从数据库中选取数据。
>
> 结果被存储在一个结果表中，称为结果集。

+ 全选

```mysql
SELECT * FROM learn.学生;
```

![image-20200321110536928](http://q7hzpu4qj.bkt.clouddn.com/image-20200321110536928.png)

+ 选取某些Column

```mysql
SELECT 姓名, 性别 FROM learn.学生;
```

![image-20200321110904547](http://q7hzpu4qj.bkt.clouddn.com/image-20200321110904547.png)

````mysql
SELECT DISTINCT 性别 FROM learn.学生;
````

去重

![image-20200321111318110](http://q7hzpu4qj.bkt.clouddn.com/image-20200321111318110.png)

### WHERE 子句

> 用于过滤记录

```mysql
SELECT column_name,column_name
FROM table_name
WHERE column_name operator value;
```

```mysql
SELECT *
FROM learn.学生
WHERE 性别='男';
```



![image-20200321113019344](http://q7hzpu4qj.bkt.clouddn.com/image-20200321113019344.png)



| 运算符  | 描述                                                       |
| :------ | :--------------------------------------------------------- |
| =       | 等于                                                       |
| <>      | 不等于。**注释：**在 SQL 的一些版本中，该操作符可被写成 != |
| >       | 大于                                                       |
| <       | 小于                                                       |
| >=      | 大于等于                                                   |
| <=      | 小于等于                                                   |
| BETWEEN | 在某个范围内                                               |
| LIKE    | 搜索某种模式                                               |
| IN      | 指定针对某个列的多个可能值                                 |

### AND & OR 运算符

> 类比条件运算符

### ORDER BY 关键字

> 对结果集进行排序

```mysql
SELECT column_name,column_name
FROM table_name
ORDER BY column_name,column_name ASC|DESC;
```

+ 默认升序

```mysql
SELECT *
FROM learn.学生
order by 姓名;
```



![image-20200321114335386](http://q7hzpu4qj.bkt.clouddn.com/image-20200321114335386.png)



+ 降序

```mysql
SELECT *
FROM learn.学生
order by 姓名 desc;
```



![image-20200321114505419](http://q7hzpu4qj.bkt.clouddn.com/image-20200321114505419.png)



* 多列(类cmp)

````mysql
SELECT *
FROM learn.学生
order by 性别, 姓名;
````

+ 注意

  + ```mysql
    order by A,B        这个时候都是默认按升序排列
    order by A desc,B   这个时候 A 降序，B 升序排列
    order by A ,B desc  这个时候 A 升序，B 降序排列
    ```

    即 **desc** 或者 **asc** 只对它紧跟着的第一个列名有效，其他不受影响，仍然是默认的升序。

### INSERT INTO 语句

> 向表中插入新记录

```mysql
insert 学生(学号,姓名,性别,专业,系别,年级,班别,出生日期,地区来源,政治面貌,民族)
values('001','李春刚','男','计算机应用','计算机','01','02','1985-2-10','呼市','团员','汉');
insert 学生(学号,姓名,性别,专业,系别,年级,班别,出生日期,地区来源,情况变动,政治面貌,民族)
values('002','东学婷','女','计算机应用','计算机','02','04','1986-10-24','包头','转系','团员','蒙');
insert 学生(学号,姓名,性别,专业,系别,年级,班别,出生日期,地区来源,情况变动,政治面貌,民族)
values('003','龙建委','男','电子商务','管理系','02','01','1984-2-17','乌海','退学','团员','蒙');
insert 学生(学号,姓名,性别,专业,系别,年级,班别,出生日期,地区来源,政治面貌,民族)
values('004','刘波','男','电子商务','管理系','03','02','1985-4-24','巴盟','团员','汉');
insert 学生(学号,姓名,性别,专业,系别,年级,班别,出生日期,地区来源,政治面貌,民族)
values('005','吴惠','女','软件开发','软件','01','01','1985-2-10','通辽','团员','汉');
insert 学生(学号,姓名,性别,专业,系别,年级,班别,出生日期,地区来源,政治面貌,民族)
values('006','王涛','男','软件开发','软件','02','02','1984-9-8','赤峰','团员','蒙');
insert 学生(学号,姓名,性别,专业,系别,年级,班别,出生日期,地区来源,政治面貌,民族)
values('007','郭凤丽','男','应用电子','电子','02','02','1984-3-2','海拉尔','团员','蒙');
insert 学生(学号,姓名,性别,专业,系别,年级,班别,出生日期,地区来源,政治面貌,民族)
values('008','贾惠','男','应用电子','电子','02','01','1983-2-2','集宁','团员','汉');
```

### UPDATE 语句

```mysql
UPDATE table_name
SET column1=value1,column2=value2,...
WHERE some_column=some_value;
```

```
update 学生
set 性别='女'
where 学号=1;
```

![image-20200321123101096](http://q7hzpu4qj.bkt.clouddn.com/image-20200321123101096.png)

### DELETE 语句

> 删除表中的行。

```mysql
DELETE FROM table_name
WHERE some_column=some_value;
```

## 进阶



## 函数

### Aggregate 函数

> 计算从列中取得的值，返回一个单一的值

- AVG() - 返回平均值
- COUNT() - 返回行数
- FIRST() - 返回第一个记录的值
- LAST() - 返回最后一个记录的值
- MAX() - 返回最大值
- MIN() - 返回最小值
- SUM() - 返回总和

### Scalar 函数

> 基于输入值，返回一个单一的值

- UCASE() - 将某个字段转换为大写
- LCASE() - 将某个字段转换为小写
- MID() - 从某个文本字段提取字符，MySql 中使用
- SubString(字段，1，end) - 从某个文本字段提取字符
- LEN() - 返回某个文本字段的长度
- ROUND() - 对某个数值字段进行指定小数位数的四舍五入
- NOW() - 返回当前的系统日期和时间
- FORMAT() - 格式化某个字段的显示方式



