# Mysql 常用操作

## 连接

```shell
  mysql -u用户名 -p密码
```

## 建库

```

CREATE DATABASE testDB; 

CREATE DATABASE testDB DEFAULT CHARSET utf8 COLLATE utf8_unicode_ci;

```

## 设置字符集

## 用户及授权

- 创建用户

  ``` Mysql
  //本地登录账户
  CREATE USER 'test'@'localhost' IDENTIFIED BY '1234';

  //远程登录账户
  CREATE USER 'test'@'%'  IDENTIFIED BY '1234'; 

  ```
  
- 授权
  
  ``` Mysql
  //授权所有权限
  grant all privileges on testDB.* to 'test'@'localhost' identified by '1234'; 
  
  //指定部分权限
  grant select,update on testDB.* to 'test'@'localhost' identified by '1234'; 
  
  //授权test用户拥有所有数据库的某些权限
  grant select,delete,update,create,drop on . to 'test'@'%' identified by '1234'; #'%' 表示对所有非本地主机授权，不包括localhost
  
  //更改授权后需刷新系统权限表
  flush privileges; 
  
  ```

- 删除用户

  ```
  //删除指定用户
  DELETE FROM mysql.user WHERE User='test' and Host='localhost'; 
  
  //删除用户后需刷新系统权限表
  flush privileges; 
  ```

## linux备份数据库脚本

```shell
-- 记录日志
echo "---------------------------------------------------" >> /serverBack/dbBack/dbBackLog.log
echo $(date +"%Y-%m-%d %H:%M:%S") "test Database backup start"  >> /serverBack/dbBack/dbBackLog.log
-- 开始备份
mysqldump -uroot -ppwd test >> /serverBack/dbBack/test_$(date +"%Y-%m-%d").sql
-- $? 判断上一次操作是否成功，备份成功返回0
if [ 0 -eq $? ];then

    if [ -f "/serverBack/dbBack/test_$(date +"%Y-%m-%d").sql" ];then
        echo $(date +"%Y-%m-%d %H:%M:%S") "test Database backup success!" >> /serverBack/dbBack/dbBackLog.log
    else
        echo $(date +"%Y-%m-%d %H:%M:%S") "test Database backup fail!" >> /serverBack/dbBack/dbBackLog.log
    fi

else
    echo $(date +"%Y-%m-%d %H:%M:%S") "test Database backup error!" >> /serverBack/dbBack/dbBackLog.log

fi

echo "---------------------------------------------------" >> /serverBack/dbBack/dbBackLog.log
-- 删除七天前的数据，防止数据冗余
find /serverBack/dbBack/ -mtime +7 -name "erms_*.sql" -exec rm -rf {} \;
-- find后面的';'不能省略
```

## mysql 多条数据合并为一行的方法

GROUP_CONCAT函数，把结果用指定分隔符拼接起来

```Mysql
SELECT GROUP_CONCAT(name SEPARATOR ',') as name from product_stock;
```

## mysql sql_mode 配置解析及修改方法

### sql_mode 配置解析

- ONLY_FULL_GROUP_BY

    对于GROUP BY聚合操作，如果在SELECT中的列，没有在GROUP BY中出现，那么这个SQL是不合法的，因为列不在GROUP BY从句中。简而言之，就是SELECT后面接的列必须被GROUP BY后面接的列所包含。如：
    
    select a,b from table group by a,b,c; (正确)
    
    select a,b,c from table group by a,b; (错误)
    
    这个配置会使得GROUP BY语句环境变得十分狭窄，所以**一般都不加这个配置**

- NO_AUTO_VALUE_ON_ZERO

    该值影响自增长列的插入。默认设置下，插入0或NULL代表生成下一个自增长值。（不信的可以试试，默认的sql_mode你在自增主键列设置为0，该字段会自动变为最新的自增值，效果和null一样），如果用户希望插入的值为0（不改变），该列又是自增长的，那么这个选项就有用了。

- STRICT_TRANS_TABLES

    在该模式下，如果一个值不能插入到一个事务表中，则中断当前的操作，对非事务表不做限制。（InnoDB默认事务表，MyISAM默认非事务表；MySQL事务表支持将批处理当做一个完整的任务统一提交或回滚，即对包含在事务中的多条语句要么全执行，要么全部不执行。非事务表则不支持此种操作，批处理中的语句如果遇到错误，在错误前的语句执行成功，之后的则不执行；MySQL事务表有表锁与行锁非事务表则只有表锁）

- NO_ZERO_IN_DATE

    在严格模式下，不允许日期和月份为零

- NO_ZERO_DATE

    设置该值，mysql数据库不允许插入零日期，插入零日期会抛出错误而不是警告。

- ERROR_FOR_DIVISION_BY_ZERO

    在INSERT或UPDATE过程中，如果数据被零除，则产生错误而非警告。如 果未给出该模式，那么数据被零除时MySQL返回NULL

- NO_AUTO_CREATE_USER

    禁止GRANT创建密码为空的用户

- NO_ENGINE_SUBSTITUTION

    如果需要的存储引擎被禁用或未编译，那么抛出错误。不设置此值时，用默认的存储引擎替代，并抛出一个异常

-  PIPES_AS_CONCAT

    将”||”视为字符串的连接操作符而非或运算符，这和Oracle数据库是一样的，也和字符串的拼接函数Concat相类似

-  ANSI_QUOTES

    启用ANSI_QUOTES后，不能用双引号来引用字符串，因为它被解释为识别符

### 修改方法

1. 语句执行

  mysql重启而恢复到我指定的配置文件的my.cnf里面设置的sql-mode选项中的内容
  
  - 全局修改

    改变全局sql_mode
  
    ``` Mysql
    -- 示例: 去掉 ONLY_FULL_GROUP_BY 重新设置值
    set @@GLOBAL.sql_mode = 'STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION';
    ```
    
  - session修改（会话有效）

    改变sql_mode
  
    ``` Mysql
    -- 示例: 去掉 ONLY_FULL_GROUP_BY 重新设置值
    set @@sql_mode = 'STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION';
    -- 语句中缺省了session， 完整的是 set @@SESSION.sql_mode
    ```

2. 直接修改数据库my.conf配置文件

  在sql_model参数中写入需要加入的sql_mode, 修改并保存之后，需要重新启动mysql

  >  示例: 去掉 ONLY_FULL_GROUP_BY
  >  [mysqld]
  >  sql_mode=’STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION’
  
## 数据被死锁锁住解锁方式

```mysql

  select concat('kill ',id,';') from information_schema.processlist t where 1=1 and t.db  = 'db_name';

```

Kill 过程中会遇上错误，跳过后成功解锁！

## 待续