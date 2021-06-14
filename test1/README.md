### 实验1： SQL语句的执行计划分析与优化指导

------

#### 实验内容

##### 1.对Oracle12c中的HR人力资源管理系统中的表进行查询与分析

查询一：

​			①：直接使用in标签限制查询部门为("IT","Sales")

​			②：通过部门名称分组

查询二：

​			①：having语句判断实现部门筛选("IT","Sales")

​			②：直接按部门名称分组

备注：以上两种查询方法都是查询部门人数及其平均工资。

##### 2.运行和分析教材中的样例（本训练任务目的是查询两个部门('IT'和'Sales')的部门总人数和平均工资，以下两个查询的结果是一样的，但效率不相同）

###### 查询一

运行结果

![](https://github.com/loveyyq/oracle/blob/master/test1/img/%E6%9F%A5%E8%AF%A2%E4%B8%80%E8%BF%90%E8%A1%8C%E7%BB%93%E6%9E%9C.png)

查询统计

![](https://github.com/loveyyq/oracle/blob/master/test1/img/%E6%9F%A5%E8%AF%A2%E4%B8%80%E7%BB%9F%E8%AE%A1.png)

###### 查询二

运行结果

![](https://github.com/loveyyq/oracle/blob/master/test1/img/%E6%9F%A5%E8%AF%A2%E4%BA%8C%E8%BF%90%E8%A1%8C%E7%BB%93%E6%9E%9C.png)

查询统计

![](https://github.com/loveyyq/oracle/blob/master/test1/img/%E6%9F%A5%E8%AF%A2%E4%BA%8C%E7%BB%9F%E8%AE%A1.png)

###### 结论分析

根据查询结果所耗时间以及自动跟踪的执行计划进行分析，查询一的语句比查询二更优。

###### 优化建议

查询一的优化指导

![](https://github.com/loveyyq/oracle/blob/master/test1/img/%E4%BC%98%E5%8C%96%E6%8C%87%E5%AF%BC.png)

建立索引

![](https://github.com/loveyyq/oracle/blob/master/test1/img/%E5%88%9B%E5%BB%BA%E7%B4%A2%E5%BC%95.png)

##### 3.设计自己的查询语句

```sql
--查询不同工作总人数以及他们的平均工资
SELECT (jobs.job_id) as "工作名称",count(employees.job_id) as "工作总人数",avg(employees.salary) as "平均工资"
from hr.jobs,hr.employees
where jobs.job_id = employees.job_id
GROUP BY jobs.job_id;
```

![](https://github.com/loveyyq/oracle/blob/master/test1/img/%E8%AE%BE%E8%AE%A1%E8%AF%AD%E5%8F%A5%E6%9F%A5%E8%AF%A2%E7%BB%93%E6%9E%9C.png)
