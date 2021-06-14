## In_Memory

- 登录自己的用户

![](https://github.com/loveyyq/oracle/blob/master/IN-Memory/img/%E7%99%BB%E5%BD%95%E8%87%AA%E5%B7%B1%E7%9A%84%E7%94%A8%E6%88%B7.jpg)

- 创建表sales

![](https://github.com/loveyyq/oracle/blob/master/IN-Memory/img/%E5%88%9B%E5%BB%BAsales%E8%A1%A8.jpg)

- 插入100万行数据

![](https://github.com/loveyyq/oracle/blob/master/IN-Memory/img/%E6%8F%92%E5%85%A5100%E4%B8%87%E6%9D%A1%E6%95%B0%E6%8D%AE.jpg)

- 进行IN_Memory前后查询对比

- IN_Memory前

![](https://github.com/loveyyq/oracle/blob/master/IN-Memory/img/in-memory%E5%89%8D.jpg)

- IN_Memory

![](https://github.com/loveyyq/oracle/blob/master/IN-Memory/img/in-memory.jpg)

- IN_Memory后

![](https://github.com/loveyyq/oracle/blob/master/IN-Memory/img/in-memory%E5%90%8E.jpg)



## 实验源码

```sql
--创建表sales，插入100万条记录
CREATE TABLE sales
   (ID NUMBER primary key, 
	NAME VARCHAR2(50 BYTE) not null, 
	QUANTITY NUMBER(8,0), 
	PRICE NUMBER(8,0)
);

--插入100万行数据
declare 
v1 number;
v2 number;
begin
    delete from sales;
    for i in 1..1000000
    loop
        v1:=dbms_random.value(1,90);
        v2:=dbms_random.value(100,900);
        insert into sales(id,name,quantity,price) values (i,'name'||i,v1,v2);
    end loop;
    commit;
end;

--插入过程中，如果遇到超出表空间 'USERS' 的空间限额，可以执行：
alter user 你的用户名 quota unlimited on users;

--进行IN-Memory前后的查询对比

--in-memory前：
--两次执行:
set autotrace on TRACEONLY 
select sum(quantity*price) total from sales;

--in-memory：
set autotrace on
alter table sales inmemory;

--in-memory后：
--两次执行:
select sum(quantity*price) total from sales;

观察consistent gets的数量，越少越快。

--查询总金额
```

