# 实验6（期末考核） 基于Oracle的铁路售票系统数据库设计

## 期末考核要求

- 自行设计一个信息系统的数据库项目，自拟铁路售票系统名称。
- 设计项目涉及的表及表空间使用方案。至少5张表和5万条数据，两个表空间。
- 设计权限及用户分配方案。至少两类角色，两个用户。
- 在数据库中建立一个程序包，在包中用PL/SQL语言设计一些存储过程和函数，实现比较复杂的业务逻辑，用模拟数据进行执行计划分析。
- 设计自动备份方案或则手工备份方案。

------

## 1.项目简介

项目名称：铁路售票系统

本项目是基于Oracle的铁路售票系统数据库设计。

涉及角色/用户：管理员、用户

涉及表：管理员表、用户表、订单表、车次表、座位表、车站表、车票信息表

车次管理功能：是由管理员进行的，主要包含车次查询、车次增加、车次修改、车次删除，主要通过操作数据库来实现这些操作。

车站管理功能：是由管理员进行的，主要包含车站查询、车站增加、车站修改、车站删除，主要通过操作数据库来实现这些操作。

用户管理功能：主要指两个方面，一个是指用户对自己的信息进行管理，包括查看、修改等操作，另一个是指管理员对用户的用户管理，包括查询用户、删除用户。

订单管理功能：是由用户进行的，主要包含查看订单、退订、改签，主要通过操作数据库来实现这些操作。

票务查询功能：是由用户进行的，主要包含车次查询、车站查询、余票查询，主要通过从数据库匹配关键信息来实现这些操作。

登录注册功能：管理员和用户可以进行登录和注册的功能。

## 2.类图设计

![](https://github.com/loveyyq/oracle/blob/master/test6/%E7%B1%BB%E5%9B%BE.png)

## 3.数据库设计

![](https://github.com/loveyyq/oracle/blob/master/test6/%E6%95%B0%E6%8D%AE%E5%BA%93.jpg)

### 3.1 admin(管理员表)

|      字段       |     类型      | 主键，外键 | 可以为空 | 默认值 | 约束 | 说明           |
| :-------------: | :-----------: | :--------: | :------: | :----: | :--: | :------------- |
|    admin_id     | Integer（20） |    主键    |    否    |        |      | 管理员ID       |
|   admin_name    | VARCHAR(100)  |            |    否    |        |      | 管理员用户名   |
| admin_password  | VARCHAR(100)  |            |    否    |        |      | 管理员密码     |
|   admin_phone   | Integer（20） |            |    否    |        |      | 管理员电话号码 |
| admin_real_name | VARCHAR(100)  |            |    否    |        |      | 管理员真实姓名 |
|  admin_address  | VARCHAR(100)  |            |    否    |        |      | 管理员居住地址 |

### 3.2user(用户表)

|   字段    |     类型      | 主键，外键 | 可以为空 | 默认值 | 约束 | 说明           |
| :-------: | :-----------: | :--------: | :------: | :----: | :--: | :------------- |
|    ID     | Integer（20） |    主键    |    否    |        |      | 用户身份证ID   |
|  account  | VARCHAR(100)  |            |    否    |        |      | 用户账号       |
| password  | VARCHAR(100)  |            |    否    |        |      | 用户密码       |
| user_name | VARCHAR(100)  |            |    否    |        |      | 用户真实姓名   |
| phone_num | Integer（20） |            |    否    |        |      | 用户手机号     |
|  E-mail   | VARCHAR(100)  |            |    否    |        |      | 用户身份证号码 |
| vip_level | Integer（10） |            |    是    |   空   |      | 用户等级       |
|  address  | VARCHAR(100)  |            |    否    |        |      | 用户地址       |

### 3.3station(车站表)

|     字段     |       类型        | 主键，外键 | 可以为空 | 默认值 | 约束 | 说明     |
| :----------: | :---------------: | :--------: | :------: | :----: | :--: | :------- |
|  station_id  |   Integer（20）   |    主键    |    否    |        |      | 车站ID   |
| station_name | VARCHAR(100 BYTE) |            |    否    |        |      | 车站姓名 |
| station_addr | VARCHAR(100 BYTE) |            |    否    |        |      | 车站地址 |

### 3.4train_order表（订单表）

|    字段     |     类型      | 主键，外键 | 可以为空 | 默认值 | 约束 | 说明       |
| :---------: | :-----------: | :--------: | :------: | :----: | :--: | :--------- |
|  order_id   | Integer（20） |    主键    |    否    |        |      | 订单ID     |
|  train_id   | VARCHAR(100)  |    外键    |    否    |        |      | 车次号     |
|    data     |     Date      |            |    否    |        |      | 出发日期   |
|   origin    | VARCHAR(100)  |            |    否    |        |      | 始发地     |
| destination | VARCHAR(100)  |            |    否    |        |      | 目的地     |
| whole_time  |     Time      |            |    否    |        |      | 总耗时     |
|  user_name  | VARCHAR(100)  |            |    否    |        |      | 乘车人名字 |
| seat_level  | VARCHAR(100)  |            |    否    |        |      | 座位等级   |
|  seat_num   | Integer（20） |            |    否    |        |      | 座位号     |
|    price    |     Float     |            |    否    |        |      | 价格       |

### 3.5train_num(车次表)

|    字段     |     类型     | 主键，外键 | 可以为空 | 默认值 | 约束 | 说明     |
| :---------: | :----------: | :--------: | :------: | :----: | :--: | :------- |
|  train_id   | VARCHAR(100) |    主键    |    否    |        |      | 车次号   |
| start_time  |     Date     |            |    否    |        |      | 出发时间 |
| arrive_time |     Date     |            |    否    |        |      | 到达时间 |
|   origin    | VARCHAR(100) |            |    否    |        |      | 始发地   |
| destination | VARCHAR(100) |            |    否    |        |      | 目的地   |
| whole_time  |     Time     |            |    否    |        |      | 总耗时   |

### 3.6seat(座位表)

|   字段    |     类型      | 主键，外键 | 可以为空 | 默认值 | 约束 | 说明       |
| :-------: | :-----------: | :--------: | :------: | :----: | :--: | :--------- |
| train_id  | VARCHAR(100)  |    外键    |    否    |        |      | 车次号     |
| spare_num | Integer（20） |            |    否    |        |      | 余座       |
| total_num | Integer（20） |            |    否    |        |      | 总的座位数 |

### 3.7ticket(车票信息表)

|     字段     |     类型      | 主键，外键 | 可以为空 | 默认值 | 约束 | 说明           |
| :----------: | :-----------: | :--------: | :------: | :----: | :--: | :------------- |
| train_id<FK> | Integer（20） |    外键    |    否    |        |      | 车次号         |
|     data     |     Date      |            |    否    |        |      | 出发日期       |
|    origin    | VARCHAR(100)  |            |    否    |        |      | 始发地         |
| destination  | VARCHAR(100)  |            |    否    |        |      | 目的地         |
|  whole_time  |     Time      |            |    否    |        |      | 总耗时         |
|  user_name   | VARCHAR(100)  |            |    否    |        |      | 乘车人姓名     |
|      ID      | Integer（20） |            |    否    |        |      | 乘车人身份证ID |
|  seat_level  | VARCHAR(100)  |            |    否    |        |      | 座位等级       |
|    price     |     Float     |            |    否    |        |      | 车票价格       |

### 3.8设计方案

##### 创建表空间：

train_admin、train_user、train_public

```sql
-- 创建表空间
CREATE TABLESPACE train_manage logging DATAFILE '/home/oracle/app/oracle/oradata/orcl/pdborcl/train_data01.dbf' size 64m autoextend on next 65m maxsize 10240m extent management local;
CREATE TABLESPACE train_user logging  DATAFILE '/home/oracle/app/oracle/oradata/orcl/pdborcl/train_data02.dbf' size 64m autoextend on next 65m maxsize 10240m extent management local;
CREATE TABLESPACE train_public logging  DATAFILE '/home/oracle/app/oracle/oradata/orcl/pdborcl/train_data03.dbf' size 200m autoextend on next 65m maxsize 10240m extent management local;
```

![](https://github.com/loveyyq/oracle/blob/master/test6/3-1.png)

##### 表空间中存放的表:

train_admin: admin

train_user: user

train_public: station、train_order、train_num、seat、ticket

```sql
-- admin	表的创建
create table admin
(
admin_id  number(20) primary key,
admin_name VARCHAR(100) not null,
admin_password VARCHAR(100) not null,
admin_phone number(20) not null,
admin_real_name VARCHAR(100) not null,
admin_address VARCHAR(100) not null
)
tablespace train_admin 
pctfree 10 
initrans 1 
maxtrans 255 
storage 
(
initial 64K 
next 1M
minextents 1 
maxextents unlimited 
);
-- user表的创建
create table user
(
ID number(20) primary key,
account VARCHAR(100) not null,
password VARCHAR(100) not null,
user_name VARCHAR(100) not null,
phone_number number(20) not null,                          
E-mail VARCHAR(100) not null,	
vip_level number(20),
address VARCHAR(100) not null,
)
tablespace train_user 
pctfree 10 
initrans 1 
maxtrans 255 
storage                           
(
initial 64K 
next 1M
minextents 1 
maxextents unlimited 
);
                          
-- station表的创建
create table station
(
station_id number(20) primary key,
station_name VARCHAR(100) not null,
station_addr VARCHAR(100) not null
)
tablespace train_public 
pctfree 10 
initrans 1 
maxtrans 255 
storage                           
(
initial 64K 
next 1M
minextents 1 
maxextents unlimited 
);
                      
-- train_order表的创建
create table train_order
(
order_id  number(20) primary key,
train_id VARCHAR(100) not null references train_num(train_id),
data Date not null,
origin VARCHAR(100) not null,
destination VARCHAR(100) not null,                    
whole_time Time not null,
user_name VARCHAR(100) not null,
seat_level VARCHAR(100) not null,
seat_num number(20) not null,
price float not null
)
tablespace train_public 
pctfree 10 
initrans 1 
maxtrans 255 
storage                           
(
initial 64K 
next 1M
minextents 1 
maxextents unlimited 
);
                        
-- train_num表的创建
create table train_num
(
train_id  VARCHAR(100) primary key,
start_time Date not null,
arrive_time Date not null,
origin VARCHAR(100) not null,
destination VARCHAR(100) not null,
whole_time Time not null
)
tablespace train_public 
pctfree 10 
initrans 1 
maxtrans 255 
storage                           
(
initial 64K 
next 1M
minextents 1 
maxextents unlimited 
);                  

-- seat表的创建
create table seat
(
train_id  VARCHAR(100) not null references train_num(train_id),
spare_num number(20) not null,
total_num number(20) not null     
)
tablespace train_public 
pctfree 10 
initrans 1 
maxtrans 255 
storage                           
(
initial 64K 
next 1M
minextents 1 
maxextents unlimited 
);                      

-- ticket表的创建
create table ticket
(
train_id  number(20) not null references train_num(train_id),
data date not null,
origin VARCHAR(100) not null,
destination VARCHAR(100) not null,
whole_time time not null,
user_name VARCHAR(100) not null,
ID number(20) not null,
seat_level VARCHAR(100) not null,
price float not null
)
tablespace train_public 
pctfree 10 
initrans 1 
maxtrans 255 
storage                           
(
initial 64K 
next 1M
minextents 1 
maxextents unlimited 
);                           
 -- 查询表空间的数据库 
select TABLE_NAME from dba_tables where TABLESPACE_NAME='TRAIN_ADMIN';
select TABLE_NAME from dba_tables where TABLESPACE_NAME='TRAIN_USER';
select TABLE_NAME from dba_tables where TABLESPACE_NAME='TRAIN_PUBLIC';
```

![](https://github.com/loveyyq/oracle/blob/master/test6/3-2.png)

##### 每个表插入数据：

总共插入数据：100000条
admin：20000条
user：20000条
station：20000条
train_order：10000条
train_num：10000条
seat：10000条
ticket：10000条

```sql
-- user表的数据插入20000条
declare 
i int;
admin_id  number(20);
admin_name VARCHAR(100);
admin_password VARCHAR(100);
admin_phone number(20);
admin_real_name VARCHAR(100);
admin_address VARCHAR(100);
begin
i:=1;
while i<=20000 
loop
admin_id:=i;
admin_name:= 'admin'|| i;
admin_password := '123'|| i;
admin_phone := '123456'|| i;
admin_real_name := '蔡超'||i;
admin_address := '成都市'||i;
insert into manage(admin_id,admin_name,admin_password,admin_phone,admin_real_name,admin_address) values (admin_id,admin_name,admin_password,admin_phone,admin_real_name,admin_address);
i:=i+1;
end loop;
commit;
end;
/


-- user表数据插入20000
declare 
i int;
ID number(20);
account VARCHAR(100);
password VARCHAR(100);
user_name VARCHAR(100);
phone_number number(20);
E-mail VARCHAR(100);
vip_level number(20);
address VARCHAR(100);
begin
i:=1;
while i<=20000 
loop
ID:='5111232000030'|| i;
account:= '123'|| i;
password := '123456'|| i;
user_name := 'cc'|| i;
phone_number := '183986'||i;
E-mail := '25122545'||i;
vip_level := '1'||i;
address := '成都市'||i;
insert into train_user(ID,account,password,user_name,phone_number,E-mail,vip_level,address) values (ID,account,password,user_name,phone_number,E-mail,vip_level,address);
i:=i+1;
end loop;
commit;
end;
/


                        
-- station表的数据插入20000条
declare 
i int;
station_id  number(20);
station_name VARCHAR(100);
station_addr VARCHAR(100);
begin
i:=1;
while i<=20000 
loop
station_id:=i;
station_name:= '名称'|| i;
station_addr := '地址'|| i;
insert into station(station_id,station_name,station_addr) values (station_id,station_name,station_addr);
i:=i+1;
end loop;
commit;
end;
/

                      
-- train_order表的数据插入10000条
declare 
i int;
order_id number(20);
train_id VARCHAR(100);
data Date;
origin VARCHAR(100);
destination VARCHAR(100);              
whole_time Time;
user_name VARCHAR(100);
seat_level VARCHAR(100);
seat_num number(20);
price float;
begin
i:=1;
while i<=10000 
loop
order_id:=i;
train_id:='123214'||i;
if i mod 6 =0 then
  data:=to_date('2015-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =1 then
  data:=to_date('2016-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =2 then
  data:=to_date('2017-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =3 then
  data:=to_date('2018-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =4 then
  data:=to_date('2019-3-2','yyyy-mm-dd')+(i mod 60);
else
  order_time:=to_date('2020-3-2','yyyy-mm-dd')+(i mod 60);
end if;
origin:= '始发地'||i;
destination:= '目的地'||i;
whole_time:=i;
user_name := 'cc'||i;
seat_level:=i;
seat_num :='B'||i mod 60;
price:='54';
insert into train_order(order_id,train_id,data,origin,destination,whole_time,user_name,seat_level,seat_num,price) values (order_id,train_id,data,origin,destination,whole_time,user_name,seat_level,seat_num,price);
i:=i+1;
end loop;
commit;
end;
/

                        
-- train_num表的数据插入10000条
declare 
i int;
train_id  VARCHAR(100);
start_time Date;
arrive_time Date;
origin VARCHAR(100);
destination VARCHAR(100);
whole_time Time;
begin
i:=1;
while i<=10000 
loop
train_id:=i;
if i mod 6 =0 then
  start_time:=to_date('2015-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =1 then
  start_time:=to_date('2016-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =2 then
  start_time:=to_date('2017-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =3 then
  start_time:=to_date('2018-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =4 then
  start_time:=to_date('2019-3-2','yyyy-mm-dd')+(i mod 60);
else
  start_time:=to_date('2020-3-2','yyyy-mm-dd')+(i mod 60);
end if;
if i mod 6 =0 then
  arrive_time:=to_date('2015-3-4','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =1 then
  arrive_time:=to_date('2016-3-4','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =2 then
  arrive_time:=to_date('2017-3-4','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =3 then
  arrive_time:=to_date('2018-3-4','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =4 then
  arrive_time:=to_date('2019-3-4','yyyy-mm-dd')+(i mod 60);
else
  arrive_time:=to_date('2020-3-4','yyyy-mm-dd')+(i mod 60);
end if;
origin:= '始发地'||i;
destination := '目的地'|| i;
whole_time := i;
insert into train_num(train_id,start_time,arrive_time,start_station,arrive_station,whole_time) values (train_id,start_time,arrive_time,start_station,arrive_station,whole_time);
i:=i+1;
end loop;
commit;
end;
/
           
-- seat表的数据的插入10000条
declare 
i int;
train_id  VARCHAR(100);
spare_num number(20);
total_num number(20);
begin
i:=1;
while i<=10000 
loop
train_id:=i;
spare_num:= i mod 60;
total_num := 60;
insert into seat(train_id,spare_num,total_num) values (train_id,spare_num,total_num);
i:=i+1;
end loop;
commit;
end;
/

-- ticket表的数据插入10000条
declare 
i int;
train_id number(20);
data date;
origin VARCHAR(100);
destination VARCHAR(100);
whole_time time;
user_name VARCHAR(100);
ID number(20);
seat_level VARCHAR(100);
price float;
begin
i:=1;
while i<=10000 
loop
train_id:='123214'||i;
if i mod 6 =0 then
  data:=to_date('2015-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =1 then
  data:=to_date('2016-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =2 then
  data:=to_date('2017-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =3 then
  data:=to_date('2018-3-2','yyyy-mm-dd')+(i mod 60);
elsif i mod 6 =4 then
  data:=to_date('2019-3-2','yyyy-mm-dd')+(i mod 60);
else
  order_time:=to_date('2020-3-2','yyyy-mm-dd')+(i mod 60);
end if;
origin:= '始发地'||i;
destination := '目的地'|| i;
whole_time := i;
user_name := 'cc'||i;
ID := '5111232000030'||i;
seat_num :='B'||i mod 60;
price:='54';
insert into ticket(train_id,data,origin,destination,whole_time,user_name,ID,seat_level,price) values (train_id,data,origin,destination,whole_time,user_name,ID,seat_level,price);
i:=i+1;
end loop;
commit;
end;
/ 

-- 查询是否插入成功
select count(*) from admin;
select count(*) from user;
select count(*) from station;
select count(*) from train_order;
select count(*) from train_num;
select count(*) from seat;
select count(*) from ticket;
```

![](https://github.com/loveyyq/oracle/blob/master/test6/3-3.png)

## 4.设计权限及用户分配方案

##### 用户：

c##train_manage 

拥有角色：c##t_manage 

分配表空间：train_admin、train_user、train_public

c##train_user 

拥有角色：c##t_user 

分配表空间：train_user、train_public

##### 角色：

c##t_manage 

拥有角色：connect、resource、dba

c##t_user 

拥有角色：connect、resource

```sql
-- 创建角色
CREATE ROLE c##t_manage;
CREATE ROLE c##t_user;
-- 授权角色
GRANT connect,resource,dba, create table,create view,create trigger, create procedure,create sequence TO c##t_manage;
GRANT connect,resource, create table,create view,create trigger, create procedure,create sequence TO c##t_user;
-- 创建用户
CREATE USER  c##train_manage  IDENTIFIED BY 123 DEFAULT TABLESPACE train_admin;
-- 指定用户额外表空间
ALTER USER c##train_manage QUOTA UNLIMITED ON train_user;
ALTER USER c##train_manage QUOTA UNLIMITED ON train_public;
-- 创建用户
CREATE USER  c##train_user   IDENTIFIED BY 123 DEFAULT TABLESPACE train_user;
-- 指定用户额外表空间
ALTER USER c##train_user QUOTA UNLIMITED ON train_public ;
-- 分配角色给用户
GRANT  c##t_manage TO  c##train_manage;
GRANT  c##t_user TO  c##train_user;
```

![](https://github.com/loveyyq/oracle/blob/master/test6/4.png)

## 5.在数据库中建立一个程序包，在包中用PL/SQL语言设计一些存储过程和函数，实现比较复杂的业务逻辑，用模拟数据进行执行计划分析。

包名： Train

函数名：Get_count(order_id_t NUMBER)

功能：输入订单ID，查询订单表,返回与该订单对应的起始车站信息

过程名：Get_orders(train_id_t VARCHAR)

功能：输入订单id，输出与该订单相关的车次的起始车站，以及统计同一时间段的车次数量并输出与订单相关的车票价格

```sql
-- 创建包
create or replace PACKAGE Train IS
  FUNCTION Get_count(order_id_t NUMBER) RETURN VARCHAR;
  PROCEDURE Get_orders(train_id_t VARCHAR);
END Train;
-- 创建函数和过程
create or replace PACKAGE BODY Train IS
    FUNCTION Get_count(order_id_t NUMBER) RETURN VARCHAR
    AS
     M VARCHAR2(100);
     N VARCHAR2(100);
     BEGIN
       select train_id into N from train_order where order_id=order_id_t;
       select origin into M from train_num where train_id=N;
       RETURN M;
     END;
    PROCEDURE Get_orders(train_id_t VARCHAR)
    AS
        N NUMBER(20);
        L date;
        S VARCHAR(100);
        R VARCHAR(100);
    begin
        --使用游标
        DBMS_OUTPUT.PUT_LINE('输出起始站：');
        select origin into R from train_num where train_id = train_id_t;
        DBMS_OUTPUT.PUT_LINE(R);
        select start_time into L from train_num where train_id = train_id_t;
        select count(*) into N from train_num where start_time = L;
        DBMS_OUTPUT.PUT_LINE('输出车次数量：');
        DBMS_OUTPUT.PUT_LINE(N);
        select price into S from ticket where train_id = train_id_t;
        DBMS_OUTPUT.PUT_LINE('输出票价：');
        DBMS_OUTPUT.PUT_LINE(S);
    END;
END TrainPack;
/
-- 测试函数
select Train.Get_count(11) AS 订单11起始车站,TrainPack.Get_count(12) AS 订单12起始车站 from dual;
-- 测试过程
DECLARE
  train_id_t VARCHAR(100);    
BEGIN
  train_id_t := 1;
  TrainPack.Get_orders (train_id_t) ;  
  train_id_t := 2;
  TrainPack.Get_orders (train_id_t) ;    
END;
```

## 6.设计自动备份方案或则手工备份方案。

本项目设置手动备份方案

- 创建恢复目录

```sql
-- 创建恢复目录：用来存储RMAN资料库的
create tablespace bp datafile '/home/oracle/app/oracle/oradata/bp.dbf' size 20m autoextend on next 5m maxsize unlimited;
-- 在恢复目录数据库中创建RMAN用户并授权
create user c##cc_r identified by 123 default tablespace bp quota unlimited on bp;
grant connect,resource,recovery_catalog_owner to c##cc_r;
```

![](https://github.com/loveyyq/oracle/blob/master/test6/6-1.png)

- 连接RMAN恢复目录数据库

```sql
-- 连接RMAN恢复目录数据库
rman catalog c##cc_r/123
-- 创建恢复目录
create catalog tablespace bp;
-- 退出
quit
-- 确认环境信息
echo $ORACLE_SID
-- 连接到目标数据库、连接到恢复目录数据库
rman catalog c##cc_r/123 target /
-- 向恢复目录注册数据库ORCL——此时就可以使用RMAN的恢复目录对目标数据库进行备份和恢复操作
register database;
```

![](https://github.com/loveyyq/oracle/blob/master/test6/6-2.png)

- 通道分配

```sql
-- 手动通道配置
run
{
allocate channel ch1 device type disk;
allocate channel ch2 device type disk;
allocate channel ch3 device type disk;
}

-- 显示已经配置过的有默认值的参数，其中包括通道参数
show all;
```

![](https://github.com/loveyyq/oracle/blob/master/test6/6-3.png)

- 归档模式下备份与恢复

```sql
-- 查看数据库是否处于归档模式下
archive log list;
-- 关闭数据库
shutdown immediate
-- 重启并设置成归档模式
startup mount;
alter database archivelog;
archive log list;
alter database open;
-- 连接到目标数据库、连接到恢复目录数据库
rman catalog c##cc_r/123 target /
-- 备份和恢复整个数据库
backup database;
```

![](https://github.com/loveyyq/oracle/blob/master/test6/6-4.png)

- 测试备份情况

```
-- 切换到保存路径
cd /home/oracle/app/oracle/recovery_area/ORCL/backupset/
-- 查看文件
ls
```

![](https://github.com/loveyyq/oracle/blob/master/test6/6-5.png)

- 测试恢复功能

```sql
-- 关闭数据库
shutdown immediate;
-- 退出数据库
exit
-- 切换到数据文件存储路径
cd /home/oracle/app/oracle/oradata/orcl/pdborcl
-- 查看数据文件
ls
-- 删除train_data01.dbf
rm -rf train_data01.dbf
-- 再次确认
ls
-- 启动数据库
sqlplus /nolog
conn /as sysdba
startup
-- 此时因为缺少数据文件无法启动
-- 检查此时数据库状态
select status from v$instance;
-- 连接RMAN
rman target sys/123
-- 恢复数据库
restore database;
-- 同步恢复
recover database;
-- 打开数据库
alter database open resetlogs;
-- 再次启动数据库，启动成功，检查此时数据库状态，此时状态已经打开
startup
select status from v$instance;
-- 再次切换到数据文件存储路径
cd /home/oracle/app/oracle/oradata/orcl/pdborcl
-- 查看数据文件，删除的已经还原
ls
```

![](https://github.com/loveyyq/oracle/blob/master/test6/6-6-1.png)

![](https://github.com/loveyyq/oracle/blob/master/test6/6-6-2.png)

![](https://github.com/loveyyq/oracle/blob/master/test6/6-6-3.png)

![](https://github.com/loveyyq/oracle/blob/master/test6/6-6-4.png)

![](https://github.com/loveyyq/oracle/blob/master/test6/6-6-5.png)

## 7.总结

​     在本次期末项目中，我自行设计了一个铁路售票系统的数据库项目。并且设计了项目涉及的表及表空间使用方案，总共设计了三个表空间、七张表，共插入了十万条数据。在设计权限及用户分配方案阶段，我设计了两类角色，两个用户。并且在数据库中建立一个程序包，在包中用PL/SQL语言设计了存储过程和函数，实现比较复杂的业务逻辑，用模拟数据进行执行计划分析，并且设计了手动备份方案，是基于RMAN设计的备份。本次项目所运用到的知识是对我们本学期所有Oracle学习的总结，其中所用到的每个知识点都是老师都在课程讲过相关的知识，因此在本次项目制作过程中，我的进展较为顺利。我认为最难的部分是备份部分，在该部分，通过尝试了几种方法后，我最终选择了RMAN设计的备份方案，因为RMAN支持多种备份手段，并且备份、恢复简单。

​    通过此次项目的独立实践，我对Oracle数据库有了进一步的理解，相信在以后的实践中能学到更多。