# Mysql
# 数据库初级
>SQL语法
## 一,DDL
### 数据库操作
1. 查询``Show DataBases;``
2. 创建 ``create database 数据库名称;``
3. 删除数据库``drop database 数据库名称;``
4. 使用数据库``use 数据库名;``
5. 查看当前使用的数据库``select database();``
### 表操作
1. 查询表查询数据库下所有表``show tables;``
2. 查询表结构``desc 表名称;``
3. 创建表
```
create table 表名 (字段名 数据类型,
                   字段名 数据类型);
```
4. 删除表``drop table 表名;``
5. 修改表修改表名``Alter table 表名 rename to 新表名；``
6. 添加列``Alter table 表名 add 列名 数据类型；``
7. 修改数据类型``Alter table 表名 modify 列名 数据类型；``
8. 修改列名，数据类型``Alter table 表名 chang 列名 新列名 新数据类型``
9. 删除列``Alter table 表名 drop 列名；``
## 二,DML
1. 表添加数据给全部列添加数据
```
insert into 表名 value(值1，值2....);
```
2. 给指定列添加数据
```
insert into 表名(列名1，列名2.......) values(值1，值2......);
```
3. 批量添加数据
```
insert into 表名 value(......),value(.......),.......;insert into 表名(列名1.....) value(值1...);
```
4. 表查询数据所有数据
```
select * from 表名表修改数据update 表名 set 列名1=值1，列名2=值2, .... where 条件;
```
5. 表删除数据
```
delete from 表名 where 条件;
```
## 三,DQL
### 查询语法
#### 1. 基础查询
1. 查询多个字段
```
#字段列表为*，则查询所有数据
select 字段列表 from 表名; 
```
2. 去除重复记录 
```
select distinct 字段列表 from 表名 ;
```
3. 起别名 AS
```
select 字段名称 as 字段别名 from 表名;
```
#### 2. 条件查询
- where in （）集合的形式以多选一where 条件 is not null 或 is null;
```
select 字段列表 from 表名 where 条件;
```
#### 3. 模糊查询
- _单个任意字符；
- %任意个数字符
```
select 学号,姓名,年级,跑步次数含免跑 from run 
                where 学号 like '____08%';
```
#### 4. 排序查询方式： 
- asc 升序；
- desc 降序
```
select 字段列表 from 表名 
order by 排序字段名1 方式，排序字段名1 方式...;
```
#### 5. 分组查询
- 将列数据作为整体进行纵向运算
- have可以对分组后条件进行过滤分页查询
<table>
<tr>
<td>聚合函数</td><td>用途</td>
</tr>
<tr><td>count</td><td>统计数量</td></tr>
<tr><td>max</td><td>找最大值</td></tr>
<tr><td>min</td><td>找最小值</td></tr>
<tr><td>sum</td><td>求和</td></tr>
<tr><td>avg</td><td>求平均</td></tr>
</table>

``` 
select 聚合函数名(列名) from 表名

select字段列表 from 表名 where 条件 
group by 分组字段名 having 条件;
```
#### 6. 分页查询
```
select 字段列表 from limit 起始索引，查询条目；
```
# 数据库高级
## 1. 约束
### 1.1 概念

* 约束是作用于表中列上的规则，用于限制加入表的数据

  例如：我们可以给id列加约束，让其值不能重复，不能为null值。

* 约束的存在保证了数据库中数据的正确性、有效性和完整性

  添加约束可以在添加数据的时候就限制不正确的数据，年龄是3000，数学成绩是-5分这样无效的数据，继而保障数据的完整性。
### 1.2 分类
1. 非空约束 NOT NULL
2. 唯一约束UNIQUE
3. 主键约束PRIMARY KEY
4. 检查约束CHECK
5. 默认约束DEFAULT
6. 外键约束FOREIGN KEY
   -  建表时添加：[constraint] [外键名称] foreign key (外键列名) references 主表名称（主表列名）
   -  建完表添加：alter table 表名 add constraint 外键名称 foreign key（外键名） reference 主表名（主表列名）
   ```
   create table class(
   id int primary key auto_increment,
   className varchar(50) unique not null
   );
   ```
### 1.3  非空约束

* 概念

  非空约束用于保证列中所有数据不能有NULL值

* 语法

    * 添加约束

      ```sql
      -- 创建表时添加非空约束
      CREATE TABLE 表名(
         列名 数据类型 NOT NULL,
         …
      ); 
      
      ```

      ```sql
      -- 建完表后添加非空约束
      ALTER TABLE 表名 MODIFY 字段名 数据类型 NOT NULL;
      ```

    * 删除约束

      ```sql
      ALTER TABLE 表名 MODIFY 字段名 数据类型;
      ```

### 1.4  唯一约束

* 概念

  唯一约束用于保证列中所有数据各不相同

* 语法

    * 添加约束

      ```sql
      -- 创建表时添加唯一约束
      CREATE TABLE 表名(
         列名 数据类型 UNIQUE [AUTO_INCREMENT],
         -- AUTO_INCREMENT: 当不指定值时自动增长
         …
      ); 
      CREATE TABLE 表名(
         列名 数据类型,
         …
         [CONSTRAINT] [约束名称] UNIQUE(列名)
      ); 
      ```

      ```sql
      -- 建完表后添加唯一约束
      ALTER TABLE 表名 MODIFY 字段名 数据类型 UNIQUE;
      ```

    * 删除约束

      ```sql
      ALTER TABLE 表名 DROP INDEX 字段名;
      ```

### 1.5  主键约束

* 概念

  主键是一行数据的唯一标识，要求非空且唯一

  一张表只能有一个主键

* 语法

    * 添加约束

      ```sql
      -- 创建表时添加主键约束
      CREATE TABLE 表名(
         列名 数据类型 PRIMARY KEY [AUTO_INCREMENT],
         …
      ); 
      CREATE TABLE 表名(
         列名 数据类型,
         [CONSTRAINT] [约束名称] PRIMARY KEY(列名)
      ); 
      
      ```

      ```sql
      -- 建完表后添加主键约束
      ALTER TABLE 表名 ADD PRIMARY KEY(字段名);
      ```

    * 删除约束

      ```sql
      ALTER TABLE 表名 DROP PRIMARY KEY;
      ```

### 1.6  默认约束

* 概念

  保存数据时，未指定值则采用默认值

* 语法

    * 添加约束

      ```sql
      -- 创建表时添加默认约束
      CREATE TABLE 表名(
         列名 数据类型 DEFAULT 默认值,
         …
      ); 
      ```

      ```sql
      -- 建完表后添加默认约束
      ALTER TABLE 表名 ALTER 列名 SET DEFAULT 默认值;
      ```

    * 删除约束

      ```sql
      ALTER TABLE 表名 ALTER 列名 DROP DEFAULT;
      ```


### 1.8  外键约束

#### 1.8.1  概述

外键用来让两个表的数据之间建立链接，保证数据的一致性和完整性。

#### 1.8.2  语法

* 添加外键约束

```sql
-- 创建表时添加外键约束
CREATE TABLE 表名(
   列名 数据类型,
   …
   [CONSTRAINT] [外键名称] FOREIGN KEY(外键列名) REFERENCES 主表(主表列名) 
); 
```

```sql
-- 建完表后添加外键约束
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称);
```

* 删除外键约束

```sql
ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
```



#### 1.8.3  练习

根据上述语法创建员工表和部门表，并添加上外键约束：

```sql
-- 删除表
DROP TABLE IF EXISTS emp;
DROP TABLE IF EXISTS dept;

-- 部门表
CREATE TABLE dept(
	id int primary key auto_increment,
	dep_name varchar(20),
	addr varchar(20)
);
-- 员工表 
CREATE TABLE emp(
	id int primary key auto_increment,
	name varchar(20),
	age int,
	dep_id int,

	-- 添加外键 dep_id,关联 dept 表的id主键
	CONSTRAINT fk_emp_dept FOREIGN KEY(dep_id) REFERENCES dept(id)	
);
```

添加数据

```sql
-- 添加 2 个部门
insert into dept(dep_name,addr) values
('研发部','广州'),('销售部', '深圳');

-- 添加员工,dep_id 表示员工所在的部门
INSERT INTO emp (NAME, age, dep_id) VALUES 
('张三', 20, 1),
('李四', 20, 1),
('王五', 20, 1),
('赵六', 20, 2),
('孙七', 22, 2),
('周八', 18, 2);
```

此时删除 `研发部` 这条数据，会发现无法删除。

删除外键

```sql
alter table emp drop FOREIGN key fk_emp_dept;
```

重新添加外键

```sql
alter table emp add CONSTRAINT fk_emp_dept FOREIGN key(dep_id) REFERENCES dept(id);
```


- 自动增长：auto_increment 当前列数字类型且唯一约束 
## 2. 数据库设计
* 数据库设计概念
    * 数据库设计就是根据业务系统的具体需求，结合我们所选用的DBMS，为这个业务系统构造出最优的数据存储模型。
    * 建立数据库中的==表结构==以及==表与表之间的关联关系==的过程。
    * 有哪些表？表里有哪些字段？表和表之间有什么关系？

* 数据库设计的步骤

    * 需求分析（数据是什么? 数据具有哪些属性? 数据与属性的特点是什么）

    * 逻辑分析（通过ER图对数据库进行逻辑建模，不需要考虑我们所选用的数据库管理系统）
    * 物理设计（根据数据库自身的特点把逻辑设计转换为物理设计）
    ![img](img/JavaWeb/d1_1.png)
    * 维护设计（1.对新的需求进行建表；2.表优化）
### 表关系
   1.  一对一
* 如：用户 和 用户详情
* 一对一关系多用于表拆分，将一个实体中经常使用的字段放一张表，不经常使用的字段放另一张表，用于提升查询性能
```
   drop table if exists tb_user;
   drop table if exists tb_user_desc;
   create table tb_user(
   id int unique ,
   nickname varchar(20),
   age int,
   gender char
   );
   create table  tb_user_desc(
   id int unique ,
   city varchar(10),
   constraint fk_tb_user foreign key (id) references tb_user(id)
   );
```   

   2. 一对多
* 如：部门 和 员工
* 一个部门对应多个员工，一个员工对应一个部门。
```
   drop table if exists emp;
   drop table if exists dept;
   -- 员工表
   create table emp(
   id int primary key auto_increment,
   name varchar(20),
   age int,
   dep_id int,
   -- 添加外键
   constraint fk_emp_dept foreign key (dep_id) references dept(id)
   );
   -- 部门表
   create table dept(
   id int primary key auto_increment,
   dept_name varchar(20) unique,
   addr varchar(20)
   );
   -- 添加两个部门
   insert into dept(dept_name, addr) VALUES ('研发部','广州'),('销售部','深圳');
   select * from dept;
   -- 添加员工
   insert into emp(name, age, dep_id) VALUES
   ('张三',20,1),
   ('李四',21,1),
   ('王五',22,1),
   ('赵六',23,2),
   ('孙七',19,2),
   ('周八',18,2);
   select * from emp;
```   
- 删除外键
```
   alter table emp drop foreign key fk_emp_dept;
```   
- 添加外键
```
   alter table emp add constraint fk_emp_dept foreign key (dep_id) references dept(id);
```   
  3. 多对多
* 如：商品 和 订单
* 一个商品对应多个订单，一个订单包含多个商品。
* 实现方式
== 建立第三张中间表，中间表至少包含两个外键，分别关联两方主键 ==

```
   drop table if exists tb_order;
   drop table if exists tb_goods;

-- 订单表
create table tb_order(
id int primary key,
payment double(10,2),
payment_type tinyint,
status tinyint
);
-- 商品表
create table tb_goods(
id int primary key auto_increment,
title varchar(100),
price double(10,2)
);
-- 中间表
create table tb_order_goods(
id int primary key auto_increment,
order_id int ,
good_id int,
count int
);
-- 添加外键
alter table tb_order_goods add constraint fk_order_id foreign key (order_id) references tb_order(id);
alter table tb_order_goods add constraint fk_goods_id foreign key (good_id) references tb_goods(id)
```
### 3. 多表查询
3.1. 内链接
> 内连接查询 ：相当于查询AB交集数据
![img](img/JavaWeb/d1_2.png)
- 隐式
```
select 字段列表 from 表名1,表名2 where
select emp.id,emp.ename,emp.salary,job.jname,job.description from emp,salarygrade,job where emp.job_id=job.id;
```
- 显式
```
select 字段列表 from 从表名1  innor join 主表名2 on
select * from emp inner join dept d on emp.dept_id = d.id;
```
3.2. 外链接
- 左链接
  左外连接：相当于查询A表所有数据和交集部分数据
```
SELECT 字段名 FROM 左表 LEFT [OUTER] JOIN 右表 ON 条件 
``` 
-  右链接
   右外连接：相当于查询B表所有数据和交集部分数据
```
SELECT 字段名 FROM 左表 RIGHRT [OUTER] JOIN 右表 ON 条件 
``` 
3.3. 子查询
概念
==查询中嵌套查询，称嵌套查询为子查询。==
>子查询根据查询结果不同，作用不同
> * 子查询语句结果是单行单列，子查询语句作为条件值，使用 =  !=  >  <  等进行条件判断
> * 子查询语句结果是多行单列，子查询语句作为条件值，使用 in 等关键字进行条件判断
> * 子查询语句结果是多行多列，子查询语句作为虚拟表
- 单行单列
```
select 字段列表 from 表 where 字段名 = （子查询）
```
- 多行单列
```
select 字段列表 from 表 where 字段名  in（子查询）
```
- 多行多列
```
select 字段列表 from （子查询） where 条件
```
```
-- 1.查询所有员工信息。查询员工编号，员工姓名，工资，职务名称，职务描述
select emp.ename,emp.salary,job.jname,job.description from emp,job where emp.job_id = job.id;
-- 2.查询员工编号，员工姓名，工资，职务名称，职务描述，部门名称，部门位置
select emp.id,emp.ename,emp.salary,job.jname,job.description,dept.dname,dept.loc from emp,job,dept where emp.job_id=job.id and emp.dept_id = dept.id;
-- 3.查询员工姓名，工资，工资等级
select emp.ename,emp.salary,salarygrade.grade from emp ,salarygrade where emp.salary>=salarygrade.losalary and emp.salary<=salarygrade.hisalary;
-- 4.查询员工姓名，工资，职务名称，职务描述，部门名称，部门位置，工资等级
select s.grade,ejd.* from salarygrade s,(select e.ename,e.salary,j.jname,j.description,d.dname,d.loc from emp e,job j,dept d where e.dept_id = d.id and e.job_id = j.id) ejd where ejd.salary>=s.losalary and ejd.salary<=s.hisalary ;
-- 5.查询出部门编号、部门名称、部门位置、部门人数
select d.id,d.dname,d.loc,e.c from dept d,(select dept_id,count(*) c from emp group by dept_id) e where d.id = e.dept_id;
```
## 事务
### 概述

> 数据库的事务（Transaction）是一种机制、一个操作序列，包含了==一组数据库操作命令==。
>
> 事务把所有的命令作为一个整体一起向系统提交或撤销操作请求，即这一组数据库命令==要么同时成功，要么同时失败==。
>
> 事务是一个不可分割的工作逻辑单元。

### 语法

* 开启事务

  ```
  START TRANSACTION;
  //或者  
  BEGIN;
  ```

* 提交事务

  ```sql
  commit;
  ```

* 回滚事务

  ```sql
  rollback;
  ```



###  代码验证

* 环境准备

  ```sql
  DROP TABLE IF EXISTS account;
  
  -- 创建账户表
  CREATE TABLE account(
  	id int PRIMARY KEY auto_increment,
  	name varchar(10),
  	money double(10,2)
  );
  
  -- 添加数据
  INSERT INTO account(name,money) values('张三',1000),('李四',1000);
  ```



* 不加事务演示问题

  ```sql
  -- 转账操作
  -- 1. 查询李四账户金额是否大于500
  
  -- 2. 李四账户 -500
  UPDATE account set money = money - 500 where name = '李四';
  
  //出现异常了...  -- 此处不是注释，在整体执行时会出问题，后面的sql则不执行
  -- 3. 张三账户 +500
  UPDATE account set money = money + 500 where name = '张三';
  ```

  整体执行结果肯定会出问题，我们查询账户表中数据，发现李四账户少了500。


* 添加事务sql如下：

  ```sql
  -- 开启事务
  BEGIN;
  -- 转账操作
  -- 1. 查询李四账户金额是否大于500
  
  -- 2. 李四账户 -500
  UPDATE account set money = money - 500 where name = '李四';
  
  // 出现异常了...  -- 此处不是注释，在整体执行时会出问题，后面的sql则不执行
  -- 3. 张三账户 +500
  UPDATE account set money = money + 500 where name = '张三';
  
  -- 提交事务
  COMMIT;
  
  -- 回滚事务
  ROLLBACK;
  ```

  上面sql中的执行成功进选择执行提交事务，而出现问题则执行回滚事务的语句。以后我们肯定不可能这样操作，而是在java中进行操作，在java中可以抓取异常，没出现异常提交事务，出现异常回滚事务。

### 4.4  事务的四大特征

* 原子性（Atomicity）: 事务是不可分割的最小操作单位，要么同时成功，要么同时失败

* 一致性（Consistency） :事务完成时，必须使所有的数据都保持一致状态

* 隔离性（Isolation） :多个事务之间，操作的可见性

* 持久性（Durability） :事务一旦提交或回滚，它对数据库中的数据的改变就是永久的

> ==说明：==
>
> mysql中事务是自动提交的。
>
> 也就是说我们不添加事务执行sql语句，语句执行完毕会自动的提交事务。
>
> 可以通过下面语句查询默认提交方式：
>
> ```java
> SELECT @@autocommit;
> ```
>
> 查询到的结果是1 则表示自动提交，结果是0表示手动提交。当然也可以通过下面语句修改提交方式
>
> ```sql
> set @@autocommit = 0;
> ```
