### 从pdborcl创建可插接数据库,简单流程

------

- 以yourdb为源数据库，yourdb已经打开为read only
- 创建自己的数据库，名称为caichao

①登录到sys用户

![](https://github.com/loveyyq/oracle/blob/master/%E7%AE%80%E5%8D%95%E6%B5%81%E7%A8%8B/%E7%99%BB%E5%BD%95sys%E7%94%A8%E6%88%B7.png)

②创建插接式数据库

![](https://github.com/loveyyq/oracle/blob/master/%E7%AE%80%E5%8D%95%E6%B5%81%E7%A8%8B/%E5%88%9B%E5%BB%BA%E6%95%B0%E6%8D%AE%E5%BA%93.png)

③打开新数据库

![](https://github.com/loveyyq/oracle/blob/master/%E7%AE%80%E5%8D%95%E6%B5%81%E7%A8%8B/%E6%89%93%E5%BC%80%E6%96%B0%E6%95%B0%E6%8D%AE%E5%BA%93.png)

④查看新数据库

![](https://github.com/loveyyq/oracle/blob/master/%E7%AE%80%E5%8D%95%E6%B5%81%E7%A8%8B/%E6%9F%A5%E7%9C%8B%E6%96%B0%E6%95%B0%E6%8D%AE%E5%BA%93.png)

⑤创建成功后，退出sys用户，以hr登录到新数据库，测试一下

![](https://github.com/loveyyq/oracle/blob/master/%E7%AE%80%E5%8D%95%E6%B5%81%E7%A8%8B/%E4%BB%A5hr%E7%99%BB%E5%BD%95%E6%96%B0%E6%95%B0%E6%8D%AE%E5%BA%93.png)

⑥查看数据库相关文件

![](https://github.com/loveyyq/oracle/blob/master/%E7%AE%80%E5%8D%95%E6%B5%81%E7%A8%8B/%E6%9F%A5%E7%9C%8B%E6%96%B0%E6%95%B0%E6%8D%AE%E5%BA%93%E7%9A%84%E7%9B%B8%E5%85%B3%E6%96%87%E4%BB%B6.png)