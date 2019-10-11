Javascript 数组 实操技术知识点记录
=============

本文记录在实际前端使用过程中遇到的一些技术点


## 二维json数组获取其中某一个key的所有数据并组成新数据返回

### 使用方法

使用map对数组进行获取指定key值数据并返回新数组


```
var defaultArr = [
 {
   "id": 1,
   "name": "Jone",
   "gender": 1,
   "age": 23
 },
 {
   "id": 2,
   "name": "Green",
   "gender": 1,
   "age": 27
 },
 {
   "id": 1,
   "name": "Xiaoming",
   "gender": 1,
   "age": 10
 }
];

var nameArrs = defaultArr.map(o => o.name);

```

## 待续