# Laravel & Lumen 常用内容记录

本文将记录在使用laravel&lumen中遇到的一些觉得可记录的内容

## Cors 跨域

  在nginx上进行配置效率会高
  ```shell
    location / {  
    
      if ($request_method = 'OPTIONS') {
        # 对于OPTIONS，不保存请求日志到日志文件
        access_log off;
    
        # 这里配置允许跨域的域名，* 代表所有，也可以写域名：http://www.xxx.com 或者IP+端口 http://192.168.1.10
        add_header 'Access-Control-Allow-Origin' '*';
        # 允许的请求类型
        add_header 'Access-Control-Allow-Methods' '*';
        add_header 'Access-Control-Allow-Credentials' true;
        add_header 'Access-Control-Allow-Headers' '*';
        # 允许跨域的最大时间，超过这个时间又会重发一次OPTIONS请求获取新的认证
        add_header 'Access-Control-Max-Age' 1728000;
        add_header 'Content-Type' 'text/plain charset=UTF-8';
        add_header 'Content-Length' 0;
        # 直接在这里返回204响应，不转发到后台服务程序
        return 204;
      }
        
      try_files $uri $uri/ /index.php$is_args$query_string;  
    }
  ```

## Collection 集合

## Eloquent 模型及关联

## Event 事件

## Job 任务

## Queue 队列

## Storage 第三方云存储

## Sms 短信

## 基于laravel框架下的实用方法

### 检查数据库表是否存在索引

#### 方法解释
  1. 参数
    - $table 数据库表名称
    - $name 数据库表中索引名称
  2. 返回数据 
    - bool true|false 有或者没有

#### 用法
```
if($this->hasIndex('test','test_email_index')){

    $table->dropIndex('test_email_index'); 
    
}
force index (idx_lx_pybm_otype_ypbm_ywybm_xykhbm_ywrqyearmonthday)
### 强制使用索引
Model::when(hasIndex('model_table_name', 'table_index_name'),function ($q){
    $q->from(DB::raw('`model_table_name` FORCE INDEX (`table_index_name`)'));
});

```

#### 方法源码
```
public function hasIndex($table, $name)
{
  $conn = Schema::getConnection();
  $dbSchemaManager = $conn->getDoctrineSchemaManager();
  $doctrineTable = $dbSchemaManager->listTableDetails($table);
  return $doctrineTable->hasIndex($name);
}
```

### 获取微秒级时间和内存使用
```php
  $time1              = microtime(true);
  $memory_get_usage1  = memory_get_usage();
  $time2              = microtime(true);
  $memory_get_usage2  = memory_get_usage();
  $result = [
      'time1' => $time1,
      'memory_get_usage1' => $memory_get_usage1,
      'time2' => $time2,
      'memory_get_usage2' => $memory_get_usage2,
      'time2 - time1' => intval(1000 * ($time2 - $time1)) . 'ms',
      'memory_get_usage2 - memory_get_usage1' => intval(($memory_get_usage2 - $memory_get_usage1) / 1024) . 'kb',
  ];
```



## 待续

### hasManyThrough
A为User B为 Org C为UserOrg 
$this->hasManyThrough(B, C,  ‘C关联A的字段’, ‘B关联C的字段’, ‘A关联C的字段’, ‘C关联B的字段’);
