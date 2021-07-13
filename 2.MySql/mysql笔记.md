## 第一天

### 1. sql, DB, DBMS 分别是什么， 他们之间的关系？

```
DB：
   DataBase (数据库， 实际上在硬盘上以文件的形似存在)
DBMS：
   Database Management System（数据库管理系统，常见的有：MySQL, Oracle DB2 Sybase, SqlServer...）
SQL:
    结构化查询语言， 是一门标准通用语言， 标准的sql语句适用于所有的数据库
```

==DBMS 负责执行 sql 语句， 通过执行 sql 语句来操作 db 中的数据==

DBMS -（执行）-> SQL 语句 -（操作）-> DB

### 2. 什么是表？

**表是数据库的基本组成单元， 所有的数据都以表格的格式组织**
一个表包括**行和列**：

行： 被称为数据/记录

列：被称为字段

- 每个字段名包含哪些信息：
  字段名， 数据类型， 相关约束

### 3. 学习通用的 SQL 语句，sql 语句分类：

`DQL（数据库查询语言）`： 查询语句， 凡是 select 语句都是 DQL

`DML（数据操作语言）`：insert /delete /update 对表当中的数据进行增删改

`DDL（数据定义语言）`：create drop alter ， 对表结构的增删改

`TCL（事务控制语言）`：commit 提交事务， rollback 回滚事务

`DCL（数据控制语言）`：grant 授权， revoke 撤销权限等

### 4.数据库导入数据

- 第 1 步. 登录 mysql 管理系统
  mysql -u 用户名 -p 密码
- 第 2 步. 查看有哪些数据库
  show databases;(这个不是 SQL 语句，属于 mysql 的命令)
  ```bash
  mysql> show databases;
  +--------------------+
  | Database           |
  +--------------------+
  | information_schema |
  | mysql              |
  | performance_schema |
  | sakila             |
  | sys                |
  | world              |
  +--------------------+
  ```
- 第 3 步. 创建属于我们自己的数据库
  create database bjpowernode(数据库名)
  ```bash
  mysql> show databases;
  +--------------------+
  | Database           |
  +--------------------+
  | information_schema |
  | bjpowernode        |
  | mysql              |
  | performance_schema |
  | sakila             |
  | sys                |
  | world              |
  +--------------------+
  ```
- 第 4 步. 使用数据库
  use bjpowernode;

- 第 5 步. 查看当前使用的数据库中有哪些表？
  show tables;
- 第 6 步. 初始化数据
  source C:\Users\qin\Desktop\bjpowernode.sql
- 第 7 步. 初始化之后数据后，查看该数据库
  ```bash
  mysql> show tables;
  +-----------------------+
  | Tables_in_bjpowernode |
  +-----------------------+
  | dept                  |
  | emp                   |
  | salgrade              |
  +-----------------------+
  3 rows in set (0.00 sec)
  ```

### 5. 什么是 sql 脚本？

> 当一个文件的扩展名是 `.sql`, 并且该问渐渐编写了大量的 sql 语句， 我们称这样的文件为 sql 脚本

_注意：可以直接使用 source 某路径下的 sql 脚本执行某个 sql 文件，进行导入数据到某个表，导入之前一定要先创建表_

### 6. 删除数据库

drop database bjpowernode;

```bash
mysql> drop database bjpowernode;
Query OK, 3 rows affected (0.02 sec)
```

### 7.查看表结构

desc 表名;

```bash
mysql> desc emp;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| EMPNO    | int(4)      | NO   | PRI | NULL    |       |
| ENAME    | varchar(10) | YES  |     | NULL    |       |
| JOB      | varchar(9)  | YES  |     | NULL    |       |
| MGR      | int(4)      | YES  |     | NULL    |       |
| HIREDATE | date        | YES  |     | NULL    |       |
| SAL      | double(7,2) | YES  |     | NULL    |       |
| COMM     | double(7,2) | YES  |     | NULL    |       |
| DEPTNO   | int(2)      | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
```

### 8. 常用命令？

- 查看当前使用的哪个数据库
  ```bash
  mysql> select database();
  ```
- 查看 mysql 版本
  ```bash
  mysql> select version();
  ```
- \c 命令， 结束一条 sql 语句
- exit 命令， 退出 mysql

### 9. 查看创建表时的 Sql 语句：

show create table 表名

<!-- sql 语句查看 -->

_sql 语句开始_

### 10. 简单的查询语句（DQL）

语法格式：
select 字段名 1,字段名 2,... from 表名;

提示：

1. 任意一条 sql 语句以 ';' 结尾。
2. sql 语句不区分大小写。

- 查询员工的年新？(字段可以参与数学运算)

```bash
mysql> select ename, sal * 12 from emp;
+--------+----------+
| ename  | sal * 12 |
+--------+----------+
| SMITH  |  9600.00 |
| ALLEN  | 19200.00 |
| WARD   | 15000.00 |
| JONES  | 35700.00 |
| MARTIN | 15000.00 |
| BLAKE  | 34200.00 |
| CLARK  | 29400.00 |
| SCOTT  | 36000.00 |
| KING   | 60000.00 |
| TURNER | 18000.00 |
| ADAMS  | 13200.00 |
| JAMES  | 11400.00 |
| FORD   | 36000.00 |
| MILLER | 15600.00 |
+--------+----------+
```

- 给查询结果的列重名

  `select ename, sal * 12 as sal from emp;`

```bash
mysql> select ename, sal * 12 as sal from emp;
```

- 别名中有中文？

```bash
mysql> select ename, sal * 12 as '年薪' from emp;
```

_注意：标准的 sql 语句，要求以单引号括起来，不要使用双引号_

- 查询所有字段？
    <!-- 实际开发中不要这样写 -->
  运行时， 会先将 `*` 转成所有的字段名， 速度比较慢

```sql
  select * from emp;
```

### 11. 条件查询

语法格式：

```sql
select 字段 1,字段 2, .... from 表名 where 条件
```

执行顺序： 先 from ， 然后 where， 最后 select

1. 查询工资等于 5000 的员工姓名？

```sql
select ename from emp where sal=5000;
```

2. 查询 SMITH 的工资？

```sql
select sal from emp where ename='SMITH';
```

3. 找出工资 大于，大于等于，小于， 小于等于 3000 的员工?

```sql
select ename from emp where sal>3000;
select ename from emp where sal>=3000;
select ename from emp where sal<3000;
select ename from emp where sal<=3000;
```

4. 找出工资不等于 3000 的员工?

```sql
select ename from emp where sal<>3000;
select ename from emp where sal!=3000;

```

5. 找出工资在 1100 和 3000 之间的员工， 包括 1100 和 3000
   and
   between....and(闭区间， 左小右大)

```sql
select ename,sal from emp where sal>=1100 and sal<=3000;
select ename,sal from emp where sal between 1100 and 3000;
```

_注意： between....and 不但可以用在数字上，还可以用在字符串上（几乎用不到）_

```sql
select ename,sal from emp where ename between 'A' and 'B';
```

6. 找出哪些人没有津贴？ 在数据库当中 NULL 不是一个值， 代表什么都没有， 为空。
   空不是一个值， 不能用等号衡量
   必须使用 `is null` 或者 `is not nul`

```sql
-- 找出哪些人津贴为NULl？
select ename,sal,comm from emp where comm is null;
-- 找出哪些人津贴不为NUll？
select ename,sal,comm from emp where comm is not null;

```

7. 找出哪些人没有津贴（NUll 和 0）

```sql
select ename,sal,comm from emp where comm is  null or comm=0;
```

8. 找出员工岗位是 MANAGER 或者 SALESMAN 的员工

```sql
select ename, job from emp where job='MANAGER' or job='SALESMAN';
```

9. and 和 or 联合使用：找出薪资大于 1000 的员工并且部门编号是 20 或者 30 的部门员工

```sql
select ename, sal, deptno from emp where sal>1000 and (deptno=20 or deptno=30);
```

_当运算符的优先级不确定的时候加小括号_

10. in 操作符(等同于 or)， 找出工作岗位是 MANAGER 和 SALESMAN 的员工?

```sql
select ename, job from emp where job in('MANAGER', 'SALESMAN');
-- 等价于下边的or
select ename, job from emp where job='MANAGER' or job='SALESMAN';
```

_注意：in 后边的两个值表示的是具体的值， 而不是一个区间_

11. not in 不在这几个值当中, 与 in 的用法相反

12. like 模糊查询
    （在模糊查询中， 必须掌握两个符号， 一个是 `%`， 一个是 `_`）
    `%` 代表多个字符， `_`代表任意一个字符

- 找出名字当中含有 o 的？

```sql
select ename from emp where ename like '%o%';
```

- 找出名字当中第二个字母是 A 的？

```sql
select ename from emp where ename like '_A%';
```

- 找出名字中有下划线的（使用转义符\）？

```sql
select ename from emp where ename like '%\_%';
```

- 找出最后一个字母是 T 的

```sql
select ename from emp where ename like '%T';
```

### 12. 排序（升序， 降序）

语法格式：

- select 字段 from 表名 order by 某个字段 asc(升序)|desc(降序)

> _注意： 数据库默认是升序_

1. 按照工资升序排， 找出员工和薪资

```sql
select ename, sal from emp order by sal;
```

2. 指定是升序还是降序？ asc 表示升序， desc 降序。

```sql
select ename, sal from emp order by sal asc;
select ename, sal from emp order by sal desc;
```

3. 案例：按照工资的降序排列， 当工资相同的时候再按照名字的升序排列？
   _注意： 按多个字段排序的时候， 谁在前边， 谁的优先级越高，后边的字段排序，只有当前边的无法完成具体的排序时，才会执行后边的排序条件_

```sql
select ename, sal from emp order by sal asc;
select ename, sal from emp order by sal desc,ename asc;
```

4. 也可以按列排序（直接使用列的序号， 不推荐使用）

```sql
select ename, sal from emp order by 1;

```

5. where 混合 排序使用

- 找出工作岗位是 SALESMAN 的员工，要求按薪资的降序排

```sql
select ename, sal from emp where job='SALESMAN' order by sal desc;
```

_执行顺序：from ---- where --- select --- order by_

### 13. 分组函数（多行处理）

- count 计数
- sum 求和
- avg 平均数
- max 最大值
- min 最小值
  _所有的分组函数， 都是对一组数据进行操作的_
  分组函数一共有 5 个。
  它的另一个名字：多行处理函数
  多行处理函数的特点： 处理多行， 最终输出的结果是一行

1. 对某个字段求和

```sql
-- 求工资总和？
select sum(sal) from emp;
-- 找出最高工资
select max(sal) from emp;
-- 找出最低工资
select min(sal) from emp;
-- 找出平均工资
select avg(sal) from emp;
-- 找出总人数
select count(*) from emp;
```

注意：

1. 分组函数自动忽略字段为 `NUll` 的数据

问题： 找出工资高于平均工资的员工？

select ename,sal from emp where sal>avg(sal);

<!-- 上述语法报错：ERROR 1111 (HY000): Invalid use of group function -->

思考为啥报错：无效的使用了分组函数
原因是：SQL 语句当中，分组函数不可直接使用在 where 字句中。 为什么？
怎么解释：
因为 group by 是在 where 执行之后才会执行

<!-- 执行顺序是 -->

```bash
select        5
    ..
from          1
    ..
where         2
    ..
group by      3
    ..
having        4
    ..
order by      6
    ..
```

那么怎么处理这个需求： 找出工资高于平均工资的员工？

```sql
-- 第1步：找出平均工资
select avg(sal) from emp;
-- 第二步：找出高于平均工资的员工
select ename,sal from emp where sal > 上一步执行的结果
```

合并上边两步的操作，使用子查询

```sql
select ename,sal from emp where sal > (select avg(sal) from emp);
```

<!-- ======== 分割线 ====== -->

- `count(*) 和 count(某个具体的字段) 他们有什么区别？`

  - `count(*):是统计的总记录条数`
  - `count(某个具体的字段):是统计当前这个字段不为NUll的数据总条数`

- 分组函数也能组合使用

```sql
select count(*),sum(sal),avg(sal) from emp;
```

### 14. 单行处理函数

输入一行， 输出一行

计算每个员工的年薪？

```sql
select ename, (sal+comm) * 12 yealsal from emp;
```

注意：sql 语句中，任何值和 NULL 运算， 结果都是 NULL

`使用 ifnull() 空处理函数？`
ifnull(可能为 NULL 的数据，被当做什么来处理)：属于单行处理函数

```sql
select ename, (sal+ifnull(comm,0)) * 12 yealsal from emp;
```

```sql
select ename, ifnull(comm,0) * 12 yealsal from emp;
```

### 15. 分组查询(group by 和 having)

- group by: 按照某个字段或者某些字段进行分组。
- having：是对分组之后的数据进行再次过滤。

案例 1. 找出每个工作岗位的最高薪资

```sql
select max(sal),job from emp group by job
+----------+-----------+
| max(sal) | job       |
+----------+-----------+
|  3000.00 | ANALYST   |
|  1300.00 | CLERK     |
|  2975.00 | MANAGER   |
|  5000.00 | PRESIDENT |
|  1600.00 | SALESMAN  |
+----------+-----------+
```

<!-- 案例2 -->

案例 2. 找出每个工作岗位的最高薪资,进行排序

```sql
mysql> select max(sal),job from emp group by job order by max(sal) desc;
+----------+-----------+
| max(sal) | job       |
+----------+-----------+
|  5000.00 | PRESIDENT |
|  3000.00 | ANALYST   |
|  2975.00 | MANAGER   |
|  1600.00 | SALESMAN  |
|  1300.00 | CLERK     |
+----------+-----------+
```

执行顺序：from --- group by ---select
_
注意：分组函数一般都会和 group by 联合使用,这也是为什么会被称为分组函数的原因，
并且任何分组函数（min，avg， max， sum， count）都是再 group by 语句执行结束之后才会执行的
当一条 sql 语句中没有 group by 的话， 整张表的数据会自成一组
_
注意：
`select ename,max(sal),job group by job;`
select 和 group by 一块使用时， 搜索的字段必须是 group by 分组后跟的字段 和 分组函数，不然上述语法再 Oracle 会报错

`规则：当一条查询语句中有 group by的话， select后面只能跟分组函数和参与分组的字段`

3. 案例 3：每个岗位的平均工资

```sql
mysql> select job,avg(sal) from emp group by job;
+-----------+-------------+
| job       | avg(sal)    |
+-----------+-------------+
| ANALYST   | 3000.000000 |
| CLERK     | 1037.500000 |
| MANAGER   | 2758.333333 |
| PRESIDENT | 5000.000000 |
| SALESMAN  | 1400.000000 |
+-----------+-------------+
```

4. 多个字段能不能联合起来一块分组？

案例：找出每个部门不同岗位的最高薪资。

```sql
mysql> select deptno,job, avg(sal) from emp group by deptno,job;
+--------+-----------+-------------+
| deptno | job       | avg(sal)    |
+--------+-----------+-------------+
|     10 | CLERK     | 1300.000000 |
|     10 | MANAGER   | 2450.000000 |
|     10 | PRESIDENT | 5000.000000 |
|     20 | ANALYST   | 3000.000000 |
|     20 | CLERK     |  950.000000 |
|     20 | MANAGER   | 2975.000000 |
|     30 | CLERK     |  950.000000 |
|     30 | MANAGER   | 2850.000000 |
|     30 | SALESMAN  | 1400.000000 |
+--------+-----------+-------------+
```

5. 找出每个部门的最高薪资， 要求显示薪资大于 2900 的数据

```sql
-- 第一步：找出mei个部门的最高薪资
mysql> select max(sal),deptno from emp group by deptno;
+----------+--------+
| max(sal) | deptno |
+----------+--------+
|  5000.00 |     10 |
|  3000.00 |     20 |
|  2850.00 |     30 |
+----------+--------+
-- 第二步：找出薪资大于2900的（以下sql执行效率低）
mysql> select max(sal),deptno from emp group by deptno having max(sal)>2900 ;
+----------+--------+
| max(sal) | deptno |
+----------+--------+
|  5000.00 |     10 |
|  3000.00 |     20 |
+----------+--------+
-- 解决第二步的效率低的sql，使用where先过滤掉，能用where解决的，不要用having
mysql> select max(sal),deptno from emp where sal>2900 group by deptno;
+----------+--------+
| max(sal) | deptno |
+----------+--------+
|  5000.00 |     10 |
|  3000.00 |     20 |
+----------+--------+
```

6. where 搞不定的，再用 having
   需求：找出每个部门的平均薪资， 要求显示薪资大于 2000 的数据

```sql
mysql> select max(sal),deptno from emp group by deptno having avg(sal)>2000;
+----------+--------+
| max(sal) | deptno |
+----------+--------+
|  5000.00 |     10 |
|  3000.00 |     20 |
+----------+--------+
```

### 16.总结一个完整的 DQL 语句怎么写？

```sql
select
    ...
from
    ...
where
    ...
group by
    ....
having
    ....
order by
    ....
```

## 遗留问题

- 1. 关于查询结果集的去重？

```sql
-- distinct去除重复记录，可以跟多个字段
select distinct job from emp;
```

2. 统计岗位的数量

```sql
-- distinct去除重复记录，可以跟多个字段
select count(distinct job) from emp;
+---------------------+
| count(distinct job) |
+---------------------+
|                   5 |
+---------------------+
```

## 第二天

<!-- 了解 -->

- 2.1 什么是连接查询？
  实际开发中，大部分的情况下都不是从但表中查询数据，一般都是多张表联合查询取出最终的结果
  在实际开发中， 一般一个业务都会对应多张表， 比如学生和班级，起码两张表。
  也就是关系型数据库表

- 2.2 表连接方式划分：

```bash
  内连接：
      等值连接
      等值连接
      自连接
  外连接
      左外连接
      右外连接
```

- 2.3 在表的连接查询方面有一种现象称为：笛卡尔积
  `笛卡尔积现象：当两张表进行连接查询的时候，没有任何条件进行限制，最后的查询结果就是两张表的乘积`
  案例：找出每一个员工的部门名称，要求显示员工名和部门
  <!-- 表别名 -->
  关于表的别名
  表别名有什么好处？
  第一： 执行效率高
  第二：可读性好

```sql
 select e.ename, d.dname from emp e,dept d;
```

- 2.4 怎么避免笛卡尔积现象？ 当然是家条件进行过滤。
  思考： 避免笛卡尔积现象， 会减少记录的匹配次数吗？
  不会， 次数还是 56 次。 只不过显示的是有效记录。

  案例：找出每一个员工的部门名称，要求显示员工名和部门

```sql
mysql> select e.ename,d.dname from emp e,dept d where e.deptno=d.deptno;
+--------+------------+
| ename  | dname      |
+--------+------------+
| SMITH  | RESEARCH   |
| ALLEN  | SALES      |
| WARD   | SALES      |
| JONES  | RESEARCH   |
| MARTIN | SALES      |
| BLAKE  | SALES      |
| CLARK  | ACCOUNTING |
| SCOTT  | RESEARCH   |
| KING   | ACCOUNTING |
| TURNER | SALES      |
| ADAMS  | RESEARCH   |
| JAMES  | SALES      |
| FORD   | RESEARCH   |
| MILLER | ACCOUNTING |
+--------+------------+
```



## MySQL常用命令

#### 1、打开MySQL， 连接数据库

```sql
mysql -uroot -p*****
```

#### 2、显示已有的数据库

```sql
show databases;
```

#### 3、创建数据库

```sql
create database + 要创建的数据库的名称;
```

#### 4、删除数据库

```sql
drop database + 要删除的数据库名称;
```

#### 5、使用数据库

```sql
use + 要使用的数据库名称;
```

#### 6、查看数据库内的表

```sql
show tables;
```

#### 7、初始化导入数据

```sql
source + sql文件的绝对路径
```

#### 8、查看表的数据结构

```sql
desc + 表的名称;
```

#### 9、查看表内的所有数据

```sql
select * from + 表名;
```

#### 10、查询当前使用的数据库

```sql
select database();
```

#### 11、查看 mysql 版本号

```sql
select version();
```

#### 12、结束一条语句

```sql
\c 或 Ctrl + c
```

#### 13、退出 mysql

```sql
exit
```

#### 14、查看创建表的 sql 语句

```
show cteate table + 表的名称;
```

#### 15、查看其他库中的表

```sql
show tables from + 数据库名称;
```



## 通用 sql 语句

#### 1、简单的查询语句（DQL）

* **语法格式**：`select 字段名1， 字段名2， 字段名3 ...... from 表名;`

 * 字段可以参与数学运算。
 * 给查询结果的列重命名：`select 字段名 as 新字段名 from 表名;`
  ==注意： 中文需要用 '' 标起来==
 * ==as 关键字可以省略。==
  	==标准SQL语句中要求字符串使用单引号括起来==
#### 2、条件查询

**语法格式**：

```
select 
	字段名1, 字段名2......
from
	表名
where
	查询条件;
```

**查询条件：**
			`between...and...`  可以使用在数据筛选也可以使用在字符串筛选。
			`is (not) null`  判断数值是否为空
			`字段名 in(值1，值2)`  等价于  `字段名 = 值1 or 字段名 = 值2`
			`not in(值1，值2...)` 不在这几个值当中
			模糊查询like：**`%` 代表任意多个字符，`_` 代表任意一个字符，如果要转义前面加`\`** 	

#### 3、排序（升序、降序）

```sql
sleect
	字段名1， 字段名2......
from 
	表名
order by
	字段名;
```

**默认是升序**，`asc` 表示**升序**， `desc` 表示**降序**（加在语句最后）
