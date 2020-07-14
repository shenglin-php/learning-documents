# Mysql 常用操作

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
## 记录日志
echo "---------------------------------------------------" >> /serverBack/dbBack/dbBackLog.log
echo $(date +"%Y-%m-%d %H:%M:%S") "test Database backup start"  >> /serverBack/dbBack/dbBackLog.log
## 开始备份
mysqldump -uroot -ppwd test >> /serverBack/dbBack/test_$(date +"%Y-%m-%d").sql
## $? 判断上一次操作是否成功，备份成功返回0
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
## 删除七天前的数据，防止数据冗余
find /serverBack/dbBack/ -mtime +7 -name "erms_*.sql" -exec rm -rf {} \;
## find后面的';'不能省略
```


## 待续