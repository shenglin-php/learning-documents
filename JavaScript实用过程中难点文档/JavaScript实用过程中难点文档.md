# Javascript 实操技术知识点记录

**本文记录在实际前端使用过程中遇到的一些技术点**

## 1. 二维json数组获取其中某一个key的所有数据并组成新数据返回

### 使用方法

使用map对数组进行获取指定key值数据并返回新数组


```javascript
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

打印结果
```javascript
["Jone", "Green", "Xiaoming"]
```

## 2. 前端富文本内容展现过程中的超过一屏幕大小图片的适配

### 使用方法

使用正则替换方式，限制图片宽度最大为外框的100%

```
// 接口或者其他地方来的富文本html内容
const oldRichText;

// 通过正则设置文中所有图片标签宽度style
const regex = new RegExp('<img', 'gi')
const newRichText = oldRichText.replace(regex, `<img style="max-width: 100%;"`)
```

## 3. 二维数组根据某个键值获取下标
```javascript
arrSelect(arr,key,val){
  if (!Array.isArray(arr)) {
    return -1;
  }
  let length = arr.length;
  if (length <= 0) {
    return -1;
  }
  if (typeof key == "undefined" || key === "") {
    return -1;
  }
  if (typeof val == "undefined") {
    return -1;
  }
  for (let i = 0; i < length; i++) {
    if (arr[i][key] == val) {
      return i;
    }
  }
  return -1;
}
```

## 4. 数组交集
```javascript
get_arr_intersect(arr1, arr2){
  let intersect_arr = arr1.filter(function(v){
      return arr2.indexOf(v)!==-1 // 利用filter方法来遍历是否有相同的元素
  })
  return intersect_arr;
}
```

## 5. 数组差集
### 所有差集
```javascript
get_all_arr_diff(arr1, arr2){
  let diff_arr = arr1.concat(arr2).filter(function (v) {
      return arr1.indexOf(v)===-1 || arr2 .indexOf(v)===-1
  })
  return diff_arr;
}
```
### 部分差集
```javascript
get_left_arr_diff(arr1, arr2){
  let diff_arr = arr1.concat(arr2).filter(function (v) {
      return arr1.indexOf(v)===-1
  })
  return diff_arr;
}
```

## 待续