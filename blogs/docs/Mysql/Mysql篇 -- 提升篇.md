---
title: Mysql篇 -- 提升篇
cover: https://pan.zealsay.com/zealsay/cover/5.jpg
date: 2021-09-02
tags:
  - mysql
categories:
  - Mysql
  - 技术笔记
---

数据库的复杂查询

<!-- more -->

存储时间：存储的是距离计算机元年(1970-1-1 0:0:0)的毫秒数(时间戳)

用 bigint 来存储速度更快

## 简单查询

1. **分页查询**
   1. 查询的结果中有太多的数据，一次显示不完可以做成分页查询
   2. 需要两个已知的条件：
      1. 当前的页码
      2. 每页显示的数量
      3. 开始的查询值=（当前页码-1）\*每页数量
      4. limit 后的数值不能加引号

```sql
select * from emp limit 开始查询的值,每页的数据量
select * from emp limit 0,5;
select * from emp limit 15,5;
select * from emp order by salary desc limit 0,5;
```

## 复杂查询

1. 聚合查询、分组查询

   1. 函数：是一个独立的功能体，需要提供若干个数据，返回结果
   2. 聚合函数：

      1. count() 数量
      2. sum() 总和
      3. avg() 平均
      4. max() 最大
      5. min() 最小

      ```sql
      select count(deptid) from emp;
      select count(eid) from emp;#使用主键列
      select sum(salary) 总工资 from emp where sex=1;
      select avg(salary) 平均工资 from emp where deptid=10;
      select ename,max(salary) from emp where sex=0;
      select min(birthday) from emp;
      ```

   3. 分组查询

      1. group by 分组指令
      2. 分组查询只能查询分组条件和聚合查询

      ```sql
      select count(eid),sum(salary),sex from emp group by sex;
      select deptid,avg(salary),max(salary),min(salary) from emp group by deptid;

      ```

   4. md5() 加密函数

      ```sql
      select md5('123456');
      ```

   5. year() 获取日期中的年份

      ```sql
      select * from emp where year(birthday)=1993;
      select * from emp where month(birthday)=12;
      select * from emp where day(birthday)=3;
      ```

   6. 子查询

      1. 是多个命令

      ```sql
      select * from emp where salary=(select max(salary) from emp);
      select * from emp where salary>(select salary from emp where ename='king');
      select * from emp where year(birthday)=year((select birthday from emp where ename='tom'))&&ename!='tom';
      select * from emp where year(birthday)=(select year(birthday) from emp where ename='tom')&&ename!='tom';
      ```

   7. 多表查询

      1. 前提是表之间是有关联的（外键和另一个表的主键）
      2. 多表查询是指查询的列分布在不同的表中

      ```sql
      #基础写法
      select ename,dname from emp,dept where deptid=did;
      select emp.ename,dept.dname from emp,dept where emp.deptid=dept.did;

      ```

   8. 新的多表查询语法

      1. 内连接

         ```sql
         select ename,dname from emp **inner** join dept on deptid=did;
         #与之前的查询结果是一样的
         ```

      2. 左外连接

         ```sql
         select ename,dname from emp **left outer join**  dept on deptid=did;
         +-------+--------+
         | ename | dname  |
         +-------+--------+
         | Tom   | 市场部 |
         | Leo   | 市场部 |
         | Lucy  | 市场部 |
         | NULL  | 测试部 |
         | Jerry | 研发部 |
         | Maria | 研发部 |
         | Black | 研发部 |
         | Peter | 研发部 |
         | Tacy  | 研发部 |
         | Lily  | 研发部 |
         | Lisa  | 研发部 |
         | King  | 研发部 |
         | tao   | 运营部 |
         | David | 运营部 |
         | Franc | 运营部 |
         | Jone  | 运营部 |
         +-------+--------+
         select dname,ename from dept left outer join  emp on deptid=did;
         #先写那个表那个表的数据全部显示
         ```

      3. 右外连接

         ```sql
         select dname,ename from dept **right outer join**  emp on deptid=did;
         select dname,ename from dept right join emp on deptid=did;**#outer可以省略**
         +--------+-------+
         | dname  | ename |
         +--------+-------+
         | 运营部 | tao   |
         | 市场部 | Tom   |
         | 研发部 | Jerry |
         | 运营部 | David |
         | 研发部 | Maria |
         | 市场部 | Leo   |
         | 研发部 | Black |
         | 研发部 | Peter |
         | 运营部 | Franc |
         | 研发部 | Tacy  |
         | 市场部 | Lucy  |
         | 运营部 | Jone  |
         | 研发部 | Lily  |
         | 研发部 | Lisa  |
         | 研发部 | King  |
         | NULL   | Brown |
         +--------+-------+
         #后写那个表那个表的数据全部显示
         (select dname,ename from dept left outer join  emp on deptid=did) union (select dname,ename from dept right join emp on deptid=did);
         (select dname,ename from dept left outer join  emp on deptid=did) union all (select dname,ename from dept right join emp on deptid=did);
         ```

      4. 全连接
         1. 左侧跟右侧左右的记录都显示
         2. mysql 不支持全连接
         3. 联合
            1. union 、合并相同的记录
            2. union all、不合并相同的记录
            3. 左外连接跟右外连接进行联合，合并相同的记录
