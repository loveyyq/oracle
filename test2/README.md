## 实验2：用户及权限管理

### 实验目的

掌握用户管理、角色管理、权根维护与分配的能力，掌握用户之间共享对象的操作技能。

### 实验内容

Oracle有一个开发者角色resource，可以创建表、过程、触发器等对象，但是不能创建视图。本训练要求：

- 在pdborcl插接式数据中创建一个新的本地角色con_res_view_loveyyq，该角色包含connect和resource角色，同时也包含CREATE VIEW权限，这样任何拥有con_res_view_loveyyq的用户就同时拥有这三种权限。
- 创建角色之后，再创建用户loveyyq，给用户分配表空间，设置限额为50M，授予con_res_view_loveyyq角色。
- 最后测试：用新用户loveyyq连接数据库、创建表，插入数据，创建视图，查询表和视图的数据。

### 实验步骤

①第一步：以system登录到pdborcl，创建角色con_res_view_loveyyq和用户loveyyq，并授权和分配空间

- 以system登录到pdborcl

![](https://github.com/loveyyq/oracle/blob/master/test2/%E7%99%BB%E5%BD%95system%E7%94%A8%E6%88%B7.png)

- 创建本地角色con_res_view_loveyyq

![](https://github.com/loveyyq/oracle/blob/master/test2/%E5%88%9B%E5%BB%BA%E8%A7%92%E8%89%B2.png)

- 授权con_res_view_loveyyq三种权限

![](https://github.com/loveyyq/oracle/blob/master/test2/%E6%8E%88%E4%BA%88%E8%A7%92%E8%89%B2%E4%B8%89%E7%A7%8D%E6%9D%83%E9%99%90.png)

- 创建用户loveyyq

![](https://github.com/loveyyq/oracle/blob/master/test2/%E5%88%9B%E5%BB%BA%E7%94%A8%E6%88%B7.png)

- 给用户分配表空间，设置限额为50M

![](https://github.com/loveyyq/oracle/blob/master/test2/%E7%BB%99%E7%94%A8%E6%88%B7%E5%88%86%E9%85%8D%E8%A1%A8%E7%A9%BA%E9%97%B4.png)

- 将用户授予给con_res_view_loveyyq角色

![](https://github.com/loveyyq/oracle/blob/master/test2/%E7%94%A8%E6%88%B7%E6%8E%88%E4%BA%88%E7%BB%99%E8%A7%92%E8%89%B2.png)

②第二步：新用户loveyyq连接到pdborcl，创建表mytable和视图myview，插入数据，最后将myview的SELECT对象权限授予hr用户。

- 新用户连接到pdborcl

![](https://github.com/loveyyq/oracle/blob/master/test2/%E8%BF%9E%E6%8E%A5%E6%96%B0%E7%94%A8%E6%88%B7.png)

- 创建表mytable

![](https://github.com/loveyyq/oracle/blob/master/test2/%E5%88%9B%E5%BB%BA%E8%A1%A8mytable.png)

- 插入数据

![](https://github.com/loveyyq/oracle/blob/master/test2/%E6%8F%92%E5%85%A5%E6%95%B0%E6%8D%AE.png)

- 创建视图myview

![](https://github.com/loveyyq/oracle/blob/master/test2/%E5%88%9B%E5%BB%BA%E8%A7%86%E5%9B%BEmyview.png)

- 将myview的SELECT对象权限授予hr用户

![](https://github.com/loveyyq/oracle/blob/master/test2/%E6%8E%88%E6%9D%83%E7%94%A8%E6%88%B7hr.png)

③第三步：用户hr连接到pdborcl，查询loveyyq授予它的视图myview

- 用户hr连接到pdborcl

![](https://github.com/loveyyq/oracle/blob/master/test2/%E7%99%BB%E5%BD%95hr.png)

- 查询loveyyq授予它的视图myview

![](https://github.com/loveyyq/oracle/blob/master/test2/%E6%9F%A5%E8%AF%A2%E8%A7%86%E5%9B%BE%E6%8E%88%E6%9D%83.png)

④第四步：测试授权给同学已经在同学的表里读写操作

- 授权同学读写表的权限

![](https://github.com/loveyyq/oracle/blob/master/test2/%E6%8E%88%E6%9D%83%E5%90%8C%E5%AD%A6%E8%AF%BB%E5%86%99%E8%A1%A8%E7%9A%84%E6%9D%83%E9%99%90.png)

- 同学在自己表里插入数据查询

![](https://github.com/loveyyq/oracle/blob/master/test2/%E5%90%8C%E5%AD%A6%E5%9C%A8%E8%87%AA%E5%B7%B1%E8%A1%A8%E9%87%8C%E7%9A%84%E6%8F%92%E5%85%A5%E6%95%B0%E6%8D%AE%E6%9F%A5%E8%AF%A2.png)

- 在同学表里读写测试

![](https://github.com/loveyyq/oracle/blob/master/test2/%E5%9C%A8%E5%90%8C%E5%AD%A6%E8%A1%A8%E4%B8%AD%E8%AF%BB%E5%86%99%E6%B5%8B%E8%AF%95.png)

### 数据库和表空间占用分析

当全班同学的实验都做完之后，数据库pdborcl中包含了每个同学的角色和用户。 所有同学的用户都使用表空间users存储表的数据。 表空间中存储了很多相同名称的表mytable和视图myview，但分别属性于不同的用户，不会引起混淆。 随着用户往表中插入数据，表空间的磁盘使用量会增加。

### 查看数据库使用情况

以下样例查看表空间的数据库文件，以及每个文件的磁盘占用情况。

```sql
$ sqlplus system/123@pdborcl

SQL>SELECT tablespace_name,FILE_NAME,BYTES/1024/1024 MB,MAXBYTES/1024/1024 MAX_MB,autoextensible FROM dba_data_files  WHERE  tablespace_name='USERS';

SQL>SELECT a.tablespace_name "表空间名",Total/1024/1024 "大小MB",
 free/1024/1024 "剩余MB",( total - free )/1024/1024 "使用MB",
 Round(( total - free )/ total,4)* 100 "使用率%"
 from (SELECT tablespace_name,Sum(bytes)free
        FROM   dba_free_space group  BY tablespace_name)a,
       (SELECT tablespace_name,Sum(bytes)total FROM dba_data_files
        group  BY tablespace_name)b
 where  a.tablespace_name = b.tablespace_name;
```

![](https://github.com/loveyyq/oracle/blob/master/test2/%E6%9F%A5%E8%AF%A2%E6%95%B0%E6%8D%AE%E5%BA%93%E4%BD%BF%E7%94%A8%E6%83%85%E5%86%B5.png)

- autoextensible是显示表空间中的数据文件是否自动增加。
- MAX_MB是指数据文件的最大容量。



