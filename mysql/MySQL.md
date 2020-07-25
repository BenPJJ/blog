# MySQL

## 查询数据（Select）

一个基本select语句分解成三个部分：查找什么数据（select）、从哪里查找（from）、查找的条件是什么（where）

```mysql
select<目标列表达式列表>
[into 新表名]
from 表名或视图名
[where<条件>]
[group by<分组表达式>]
[order by<排序表达式>[ASC|DESC]]
```

### 查询指定的列

- 查询表中所有列

  > select * from tb_name;

- 查询表中指定的列

  > select tb_name.<字符型字段>,<字符型字段>... from tb_name

- 指定查询结果中的列标题

## 连接查询

### 定义

若一个查询同时涉及两个或两个以上的表，则称之为连接查询，连接查询可分为内连接、外连接和交叉连接

- 内连接（inner join on）

  内连接使用比较运算符对两个表中的数据进行比较，并列出与连接条件匹配的数据行，组合成新的记录。结果只保留满足条件的记录

  > select a列1,a列2,...a列n,b列1,b列2,...b列n from a inner join b on 条件;

- 外连接

  外连接的返回结果中不仅包含符合连接条件的行，还会包括左表、右表或两个表中的所有数据行，这两种情况分别称为左连接、右连接

  - 左连接（left join on）

    左表保持不动，右表在右侧滑动，用右表匹配左表。结果保留左表的所有行，右表中不匹配的行默认填充为空值NULL

    > select a列1,a列2,...a列n,b列1,b列2,...b列n from a left join b on 条件;

  - 右连接（right join on）

    同左连接相反

- 交叉连接

  交叉连接的返回结果是第一个表中符合查询条件的数据行乘以第二个表中符合查询条件的数据行数，即两个表中所有数据的组合

## 联合查询

union与union all的区别：union会把多个查询语句的结果合并后去重，union all会保留所有的查询结果

> select c_Name from members where c_adress='重庆' union select c_Name from members where c_address='浙江杭州'