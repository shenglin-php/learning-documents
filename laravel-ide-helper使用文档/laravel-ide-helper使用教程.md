# laravel-ide-helper扩展使用

代码提示及补全工具扩展，使开发过程更方便。
[扩展下载地址](https://github.com/barryvdh/laravel-ide-helper)

## 安装

```
# 如果只想在开发环境安装请加上 --dev
composer require barryvdh/laravel-ide-helper

# 在为模型注释字段的时候必须用到下面的扩展 如果只想在开发环境安装请加上 --dev
composer require "doctrine/dbal: ^2.9"
```

> 如果是使用的环境是laravel v5.5及以上版本，框架会自动注册provider<br/>
> 使用lumen或者laravel v5.5以下版本， 请自行在config/app.php文件中手动注册provider
```
	Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class
```

## 使用
```
#为 Facades 生成注释
php artisan ide-helper:generate

#为数据模型生成注释
php artisan ide-helper:models

#生成 PhpStorm Meta file
php artisan ide-helper:meta 

#为单个数据模型生成注释
php artisan ide-helper:models 
```