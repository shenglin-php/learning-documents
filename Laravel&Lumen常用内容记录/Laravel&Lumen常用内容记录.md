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

## 待续

