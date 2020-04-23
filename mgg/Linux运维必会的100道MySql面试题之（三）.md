**001：请解释关系型数据库概念及主要特点？**

关系型数据库模型是把复杂的数据结构归结为简单的二元关系，对数据的操作都是建立一个 或多个关系表格上

最大的特点就是二维的表格，通过SQL结构查询语句存取数据，保持数据 一致性方面很强大

**002：请说出关系型数据库的典型产品、特点及应用场景？**

mysql 互联网企业常用

oracle 大型传统企业应用软件

如数据备份、复杂连接查询、一致性数据存储等，还是使用MySQL或者其他传统的关系型数据库最合适

**003：请解释非关系型数据库概念及主要特点？**

非关系型数据库也被称为NoSQL数据库，数据存储不需有特有固定的表结构

特点：高性能、高并发、简单易安装

**004：请说出非关系型数据库的典型产品、特点及应用场景？**

memcaced 纯内存

redis 持久化缓存

mongodb 面向文档

如果需要短时间响应的查询操作，没有良好模式定义的数据存储，或者模式更改频繁的数据存储还是用NoSQL

**005：请详细描述SQL语句分类及对应代表性关键字**

sql语句分类如下

DDL 数据定义语言，用来定义数据库对象：库、表、列

```
代表性关键字：create alter drop
```

DML 数据操作语言，用来定义数据库记录

```
代表性关键字:insert delete update
```

DCL 数据控制语言，用来定义访问权限和安全级别

```
代表性关键字:grant deny revoke
```

DQL 数据查询语言，用来查询记录数据

```
代表性关键字:select 
```

**006：请详细描述char(4)和varchar(4)的差别**

char长度是固定不可变的，varchar长度是可变的（在设定内）

比如同样写入cn字符，char类型对应的长度是4(cn+两个空格),但varchar类型对应长度是2

**007：如何创建一个utf8字符集的数据库mingongge?**

create database mingongge default character utf8 collate utf8_general_ci;

**008：如何授权mingongge用户从172.16.1.0/24访问数据库**

grant all on *.* to mingongge@'172.16.1.0/24' identified by '123456';

**009：什么是MySQL多实例，如何配置MySQL多实例?**

mysql多实例就是在同一台服务器上启用多个mysql服务，它们监听不同的端口，运行多个服务进程

它们相互独立，互不影响的对外提供服务，便于节约服务器资源与后期架构扩展

多实例的配置方法有两种：

1、一个实例一个配置文件，不同端口

2、同一配置文件(my.cnf)下配置不同实例，基于mysqld_multi工具

具体配置请参考之前的文章

**010：如何加强MySQL安全，请给出可行的具体措施?**

1、删除数据库不使用的默认用户

2、配置相应的权限（包括远程连接）

3、不可在命令行界面下输入数据库的密码

4、定期修改密码与加强密码的复杂度

**011：MySQL root密码忘了如何找回？**

```
mysqld_safe --skip-grant-tables &   #启动数据库服务

mysql -uroot -ppassowrd -e "use mysql;update user set passowrd = PASSWORD('newpassword') where user = 'root';flush privileges;"
```

**012：delete和truncate删除数据的区别？**

前者删除数据可以恢复，它是逐条删除速度慢

后者是物理删除，不可恢复，它是整体删除速度快

**013：MySQL Sleep线程过多如何解决？**

1、可以杀掉sleep进程，kill PID

2、修改配置，重启服务

```
[mysqld]

wait_timeout = 600

interactive_timeout=30

如果生产服务器不可随便重启可以使用下面的方法解决

set global wait_timeout=600

set global interactive_timeout=30;
```

**014：sort_buffer_size参数作用？如何在线修改生效？**

在每个connection(session)第一次连接时需要使用到，来提访问性能

```
set global sort_buffer_size = 2M
```

**015：如何在线正确清理MySQL binlog？**

MySQL中的binlog日志记录了数据中的数据变动，便于对数据的基于时间点和基于位置的恢复,但日志文件的大小会越来越大，点用大量的磁盘空间，因此需要定时清理一部分日志信息

手工删除：

```
首先查看主从库正在使用的binlog文件名称 


show master(slave) status\G


删除之前一定要备份


purge master logs before'2017-09-01 00:00:00'; 


#删除指定时间前的日志

purge master logs to'mysql-bin.000001';

#删除指定的日志文件
```

自动删除：

```
通过设置binlog的过期时间让系统自动删除日志

show variables like 'expire_logs_days'; 

set global expire_logs_days = 30;

#查看过期时间与设置过期时间
```

**016：Binlog工作模式有哪些？各什么特点，企业如何选择？**

1.Row(行模式)

日志中会记录成每一行数据被修改的形式，然后在slave端再对相同的数据进行修改

2.Statement(语句模式)

每一条修改的数据都会完整的记录到主库master的binlog里面，在slave上完整执行在master执行的sql语句

3.mixed(混合模式)

结合前面的两种模式，如果在工作中有使用函数 或者触发器等特殊功能需求的时候，使用混合模式

数据量达到比较高时候，它就会选择 statement模式，而不会选择Row Level行模式

**017：误操作执行了一个drop库SQL语句，如何完整恢复？**

1、停止主从复制，在主库上执行锁表并刷新binlog操作，接着恢复之前的全备文件（比如0点的全备）

2、将0点时的binlog文件与全备到故障期间的binlog文件合并导出成sql语句

```
mysqlbinlog --no-defaults mysql-bin.000011 mysql-bin.000012 >bin.sql
```

3、将导出的sql语句中drop语句删除，恢复到数据库中

```
mysql -uroot -pmysql123 < bin.sql
```

**018：mysqldump备份使用了-A -B参数，如何实现恢复单表？**

-A 此参数作用是备份所有数据库（相当于--all-databases）

-B databasename 备份指定数据（单库备份使用）

备份时指定数据库与表名即可在恢复时只恢复单表

**019：详述MySQL主从复制原理及配置主从的完整步骤**

主从复制的原理如下：

主库开启binlog功能并授权从库连接主库，从库通过change master得到主库的相关同步信息然后连接主库进行验证，主库IO线程根据从库slave线程的请求，从master.info开始记录的位置点向下开始取信息，同时把取到的位置点和最新的位置与binlog信息一同发给从库IO线程,从库将相关的sql语句存放在relay-log里面，最终从库的sql线程将relay-log里的sql语句应用到从库上，至此整个同步过程完成，之后将是无限重复上述过程

完整步骤如下：

1、主库开启binlog功能，并进行全备，将全备文件推送到从库服务器上

2、show master statusG 记录下当前的位置信息及二进制文件名

3、登陆从库恢复全备文件

4、执行change master to 语句

5、执行start slave and show slave statusG

点击关注 **[民工哥技术之路](http://mp.weixin.qq.com/mp/homepage?__biz=MzI0MDQ4MTM5NQ==&hid=8&sn=1db566bed001a8db6d9927540ccc2156&scene=18#wechat_redirect)** 微信公众号对话框回复关键字：1024 可以获取一份最新整理的技术干货：包括系统运维、数据库、redis、MogoDB、电子书、Java基础课程、Java实战项目、架构师综合教程、架构师实战项目、大数据、Docker容器、ELK Stack、机器学习、BAT面试精讲视频等。