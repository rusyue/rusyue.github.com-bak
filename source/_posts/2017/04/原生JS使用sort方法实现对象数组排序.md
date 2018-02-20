---
title: 原生JS使用sort方法实现对象数组排序
date: 2017-04-03 20:05:57
categories:
    - 前端
tags:
    - 前端
    - 随笔
    - JavaScript
---

sort 方法接受一个特殊的比较函数作为参数，这个比较函数又有 a, b 两个参数，这两个参数其实就是数组里每一个元素，每次会抽出两个元素进行比较，同时根据比较函数的返回值对这两个元素进行排序，排序有三种情况：
- 返回值 = 0时，a, b 位置不变
- 返回值 < 0时，a 排在 b 前面
- 返回值 > 0时，b 排在 a 前面

<!-- more -->

```javascript
/**
 * 利用sort实现对象数组排序
 * 调用: employees.sort( by(param) )
 * 函数by: 根据param对对象中对应的键值进行比较，按sort方法的规则返回正负数
 * by调用: by( param1, by(param2) ), param1比较结果相同时按param2进行比较
 */

var employees=[];
employees[0]={name:"George", age:32, retiredate:"March 12, 2014"};
employees[1]={name:"Edward", age:17, retiredate:"June 2, 2023"};
employees[4]={name:"Adward", age:17, retiredate:"June 2, 2023"};
employees[2]={name:"Christine", age:58, retiredate:"December 20, 2036"};
employees[3]={name:"Sarah", age:62, retiredate:"April 30, 2020"};


var by = function(key, fn) {
  return function (o,p) {
    var a,b;
    if (typeof o === 'object' && typeof p === 'object' && o && p) {
      a = o[key];
      b = p[key];
      if (a === b) {
        return typeof fn === 'function' ? fn(o,p) : 0;
      }
      if (typeof a === typeof b) {
        return a < b ? -1 : 1;
      }
      return typeof a < typeof b ? -1 : 1;
    }
  };
}

employees.sort(by('age',by('name')));
console.log(employees);

/**
 * 利用sort实现对象数组排序
 * 调用: employees.sort( by(param) )
 * 函数by: 根据param对对象中对应的键值进行比较，按sort方法的规则返回正负数
 * by调用: by( param1, by(param2) ), param1比较结果相同时按param2进行比较
 */

var employees=[];
employees[0]={name:"George", age:32, retiredate:"March 12, 2014"};
employees[1]={name:"Edward", age:17, retiredate:"June 2, 2023"};
employees[4]={name:"Adward", age:17, retiredate:"June 2, 2023"};
employees[2]={name:"Christine", age:58, retiredate:"December 20, 2036"};
employees[3]={name:"Sarah", age:62, retiredate:"April 30, 2020"};


var by = function(key, fn) {
  return function (o,p) {
    var a,b;
    if (typeof o === 'object' && typeof p === 'object' && o && p) {
      a = o[key];
      b = p[key];
      if (a === b) {
        return typeof fn === 'function' ? fn(o,p) : 0;
      }
      if (typeof a === typeof b) {
        return a < b ? -1 : 1;
      }
      return typeof a < typeof b ? -1 : 1;
    }
  };
}

employees.sort(by('age',by('name')));

console.log(employees);
/*
输出：
[ { name: 'Adward', age: 17, retiredate: 'June 2, 2023' },
  { name: 'Edward', age: 17, retiredate: 'June 2, 2023' },
  { name: 'George', age: 32, retiredate: 'March 12, 2014' },
  { name: 'Christine', age: 58, retiredate: 'December 20, 2036' },
  { name: 'Sarah', age: 62, retiredate: 'April 30, 2020' } ]
*/
```
