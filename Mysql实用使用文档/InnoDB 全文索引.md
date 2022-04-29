# InnoDB之全文索引

[mysql查询text innerdb_mysql 5.7版本 InnoDB支持全文索引？](https://blog.csdn.net/weixin_39669075/article/details/113614017)


### 基本版本要求
  - > 5.7.6 支持中文全文索引 创建索引时需要用到 with parser ngram

### 实现方案 

```mysql
# 给已存在表添加索引

ALERT table_name ADD FULLTEXT INDEX idx_indexname (column_name...) WITH PARSER ngram;

# 或者

CREATE FULLTEXT INDEX idx_indexname ON table_name (column_name...) WITH PARSER ngram;
```

### 需要设置全文索引的列

 - 被常用模糊搜索 且 无法确定关键字位置

### 查询方式

1. 布尔模式 IN BOOLEAN MODE

  - “+”表示必须包含
  - “-”表示必须排除
  - “>”表示出现该单词时增加相关性
  - “<”表示出现该单词时降低相关性
  - “*”表示通配符
  - “""”表示短语
  - “~”允许出现该单词，但是出现时相关性为负

  ```sql
  match(shdz) against('关键字' in boolean mode)
  ```
  
2. 自然语言模式 IN NATURAL LANGUAGE MODE

  ```sql
  match(shdz) against('关键字' in natual language mode)
  ```