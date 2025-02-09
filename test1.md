实验1：SQL语句的执行计划分析与优化指导
实验目的：
分析SQL执行计划，执行SQL语句的优化指导。理解分析SQL语句的执行计划的重要作用。

实验内容：
对Oracle12c中的HR人力资源管理系统中的表进行查询与分析。
首先运行和分析教材中的样例：本训练任务目的是查询两个部门('IT'和'Sales')的部门总人数和平均工资，以下两个查询的结果是一样的。但效率不相同。
设计自己的查询语句，并作相应的分析，查询语句不能太简单。
教材中的查询语句

查询1：

set autotrace on

SELECT d.department_name,count(e.job_id)as "部门总人数",
avg(e.salary)as "平均工资"
from hr.departments d,hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT','Sales')
GROUP BY d.department_name;

查询2：
set autotrace on

SELECT d.department_name,count(e.job_id)as "部门总人数",
avg(e.salary)as "平均工资"
FROM hr.departments d,hr.employees e
WHERE d.department_id = e.department_id
GROUP BY d.department_name
HAVING d.department_name in ('IT','Sales');

分析：人们在使用SQL时往往会陷入一个误区，即太关注于所得的结果是否正确，
而忽略了不同的实现方法之间可能存在的性能差异，这种性能差异在大型的或是
复杂的数据库环境中（如联机事务处理OLTP或决策支持系统DSS）中表现得尤为
明显。据了解，不良的SQL往往来自于不恰当的索引设计、不充份的连接条件和
不可优化的where子句。在对它们进行适当的优化后，其运行速度有了明显地提高！
所谓优化即where子句利用了索引，不可优化即发生了表扫描或额外开销
在 SQL 中增加 HAVING 子句原因是，WHERE 关键字无法与聚合函数一起使用。
HAVING 子句可以让我们筛选分组后的各组数据。

教材： 查询1与查询2比少了HAVING子句，HAVING 子句可以让我们筛选分组后的各组数据。
我觉得查询2使用HAVING子句是没有必要的，having与where最大的区别是having 能带聚合函
数，而where不可以，而索要查询的的没必要使用having字句。

设计与分析：
set autotrace on

SELECT d.department_name,count(e.job_id)as "部门总人数",
avg(e.salary)as "平均工资"
from hr.departments d,hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT','Sales')
GROUP BY d.department_name;

查询两个部门('IT'和'Sales')的部门总人数和平均工资


