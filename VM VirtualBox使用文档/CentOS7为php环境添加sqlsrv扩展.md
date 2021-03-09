1. 移除unixODBC版本
```shell
yum remove unixODBC
```

2. [加入微软源](https://packages.microsoft.com/config/rhel/7/)
```shell
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssqlrelease.repo
```

3. 安装驱动
```shell
yum install msodbcsql mssql-tools unixODBC-devel
```

4. [下载pdo_sqlsrv扩展包](http://pecl.php.net/package/pdo_sqlsrv)
```shell
wget http://pecl.php.net/get/pdo_sqlsrv-5.9.0.tgz
```

5. 解压安装
```shell
tar -zxvf pdo_sqlsrv-5.9.0.tgz
cd pdo_sqlsrv-5.9.0
```

6. 使用对应版本的phpize安装扩展
```shell
/www/server/php/74/bin/phpize ./configure --with-php-config=/www/server/php/74//bin/php-config make && make install
```

7. [扩展文件下载](https://github.com/Microsoft/msphpsql/releases)

选择对应的版本

选择复制对应的四个文件（线程安全或非线程安全）到extension_dir(/www/server/php/74/lib/php/extensions/no-debug-non-zts-20190902/)路径地址的下面

8. 配置php.ini

打开php.ini文件

/www/server/php/74/etc/php.ini

添加扩展文件
extension=php_sqlsrv_74_nts.so
extension=php_pdo_sqlsrv_74_nts.so

重启服务即可