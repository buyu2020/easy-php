**01 如何启动MySql服务**

```
 /etc/init.d/mysqld start
 service mysqld start
```

Centos 7.x 系统

```
sysctl start mysqld
```

**02 检测端口是否运行**

```
 lsof -i :3306
 netstat -lntup |grep 3306
```

![img](https://segmentfault.com/img/remote/1460000020785840)
**03 设置或修改MySql密码**
设置密码

```
mysql -uroot -ppassword -e "set passowrd for root = passowrd('passowrd')"
mysqladmin -uroot passowrd "NEWPASSWORD"
```

更改密码

```
mysqladmin -uroot passowrd oldpassowrd "NEWPASSWORD"
use mysql;
update user set passowrd = PASSWORD('newpassword') where user = 'root';flush privileges;
```

msyql 5.7以上版本修改默认密码命令

```
alter user 'root'@'localhost' identified by 'root'
```

**04 登陆数据库**

```
mysql -uroot -ppassword
```

**05 查看当前数据库的字符集**

```
show create database DB_NAME;
```

**06 查看当前数据库版本**

```
mysql -V
mysql -uroot -ppassowrd -e "use mysql;select version();"
```

![img](https://segmentfault.com/img/remote/1460000020785841)
**07 查看当前登录用户**

```
mysql -uroot -ppassowrd -e "select user();"
```

![img](https://segmentfault.com/img/remote/1460000020785842)

```
select user(); #进入数据库查询
```

**08 创建GBK字符集数据库mingongge并查看完整创建语句**

```
create database mingongge default charset gbk collate gbk_chinese_ci;
```

**09 创建用户mingongge使用之可以管理数据库mingongge**

```
grant all on mingongge.* to 'mingongge'@'localhost' identified by 'mingongge';
```

**10 查看创建用户mingongge的权限**

```
show grants for mingongge@localhost;
```

![img](https://segmentfault.com/img/remote/1460000020785843)

**11 查看当前数据库有哪此用户**

```
select user from mysql.user;
```

**12 进入mingongge数据库**

```
use mingongge
```

![img](https://segmentfault.com/img/remote/1460000020785844)

**13 创建一个innodb GBK表test,字段id int(4)和name varchar(16)**

```
create table test (
 id int(4),
  name varchar(16)
 )ENGINE=innodb DEFAULT CHARSET=gbk;
```

**14 查看建表结构及表结构的SQL语句**

```
desc test;
show create table test\G
```

![img](https://segmentfault.com/img/remote/1460000020785845)
**15插入一条数据“1,mingongge”**

```
insert into test values('1','mingongge');
```

**16 再批量插入2行数据“2,民工哥”,“3,mingonggeedu”**

```
insert into test values('2','民工哥'),('3','mingonggeedu');
```

**17 查询名字为mingongge的记录**

```
select * from test where name = 'mingongge';
```

![img](https://segmentfault.com/img/remote/1460000020785846)
**18 把数据id等于1的名字mingongge更改为mgg**

```
update test set name = 'mgg' where id = '1';
```

**19 在字段name前插入age字段，类型tinyint(2)**

```
alter table test add age tinyint(2) after id;
```

![img](https://segmentfault.com/img/remote/1460000020785847)
**20 不退出数据库,完成备份mingongge数据库**

```
system mysqldump -uroot -ppassword -B mingongge >/root/mingongge_bak.sql
```

![img](https://segmentfault.com/img/remote/1460000020785848)

点击关注 [民工哥技术之路](https://mp.weixin.qq.com/s/ivP9E07U-YWd7UVNDZQgXQ) 微信公众号对话框回复关键字：1024 可以获取一份最新整理的技术干货：包括系统运维、数据库、redis、MogoDB、电子书、Java基础课程、Java实战项目、架构师综合教程、架构师实战项目、大数据、Docker容器、ELK Stack、机器学习、BAT面试精讲视频等。