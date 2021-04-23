# Laravel & Lumen 常用内容记录

本文将记录在使用laravel&lumen中遇到的一些觉得可记录的内容

## Cors 跨域

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

A为User B为UserOrg C为 Org
$this->hasManyThrough(B, C, ‘B关联A的字段’, ‘A关联B的字段’, ‘C关联B的字段’, ‘B关联C的字段’);
