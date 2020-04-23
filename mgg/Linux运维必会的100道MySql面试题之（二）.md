**21.删除test表中的所有数据，并查看**

```
delete from test;

select * from test;
```

![img](https://segmentfault.com/img/remote/1460000020863244)

**22.删除表test和mingongge数据库并查看**

```
drop table test;

show tables;

drop database mingongge;

show databases;
```

![img](https://segmentfault.com/img/remote/1460000020863245)

**23.不退出数据库恢复以上删除的数据**

```
system mysql -uroot -pMgg123.0. </root/mingongge_bak.sql
```

![img](https://segmentfault.com/img/remote/1460000020863246)

**24.把库表的GBK字符集修改为UTF8**

```
alter database mingongge default character set utf8;

alter table test default character set utf8;
```

![img](https://segmentfault.com/img/remote/1460000020863247)

**25.把id列设置为主键，在Name字段上创建普通索引**

```
 alter table test add primary key(id);

create index mggindex on test(name(16));
```

![img](https://segmentfault.com/img/remote/1460000020863249)

**26.在字段name后插入手机号字段(shouji)，类型char(11)**

```
alter table test add shouji char(11);

#默认就是在最后一列后面插入新增列
```

![img](https://segmentfault.com/img/remote/1460000020863250)

**27.所有字段上插入2条记录（自行设定数据）**

```
insert into test values('4','23','li','13700000001'),('5','26','zhao','13710000001');
```

![img](https://segmentfault.com/img/remote/1460000020863251)

**28.在手机字段上对前8个字符创建普通索引**

```
create index SJ on test(shouji(8));
```

29.查看创建的索引及索引类型等信息

```
show index from test;

show create table test\G

#下面的命令也可以查看索引类型     

show keys from test\G  
```

![img](https://segmentfault.com/img/remote/1460000020863252)

**30.删除Name，shouji列的索引**

```
drop index SJ on test;

drop index mggindex on test;
```

![img](https://segmentfault.com/img/remote/1460000020863253)

**31.对Name列前6个字符以及手机列的前8个字符组建联合索引**

```
create index lianhe on test(name(6),shouji(8));
```

![img](https://segmentfault.com/img/remote/1460000020863254)

**32.查询手机号以137开头的，名字为zhao的记录（提前插入）**

```
select * from test where shouji like '137%' and name = 'zhao';
```

![img](https://segmentfault.com/img/remote/1460000020863255)

**33.查询上述语句的执行计划（是否使用联合索引等）**

```
explain select * from test where name = 'zhao' and shouji like '137%'\G
```

![img](https://segmentfault.com/img/remote/1460000020863256)

**34.把test表的引擎改成MyISAM**

```
alter table test engine=MyISAM;
```

![img](https://segmentfault.com/img/remote/1460000020863257)

**35.收回mingongge用户的select权限**

```
revoke select on mingongge.* from mingongge@localhost;
```

![img](https://segmentfault.com/img/remote/1460000020863258)

**36.删除mingongge用户下数据库mingongge**

```
drop user migongge@localhost;

drop database mingongge;
```

![img](https://segmentfault.com/img/remote/1460000020863259)

**37.使用mysqladmin关闭数据库**

```
mysqladmin -uroot -pMgg123.0. shutdown

lsof -i :3306
```

**38.MySQL密码丢了，请找回？**

```
mysqld_safe --skip-grant-tables &   
#启动数据库服务

mysql -uroot -ppassowrd -e "use mysql;update user set passowrd = PASSWORD('newpassword') where user = 'root';flush privileges;"
```

点击关注 **[民工哥技术之路](http://mp.weixin.qq.com/mp/homepage?__biz=MzI0MDQ4MTM5NQ==&hid=8&sn=1db566bed001a8db6d9927540ccc2156&scene=18#wechat_redirect)** 微信公众号对话框回复关键字：1024 可以获取一份最新整理的技术干货：包括系统运维、数据库、redis、MogoDB、电子书、Java基础课程、Java实战项目、架构师综合教程、架构师实战项目、大数据、Docker容器、ELK Stack、机器学习、BAT面试精讲视频等。