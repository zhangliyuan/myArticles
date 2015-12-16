title: Javascript定义全局变量的三种方式
date: 2015-10-11 07:50:17
tags:JavaScript 
---

### 方式1
```javascript
var test = 5;
```
这种方式是直接写在js文件中，不能被包含在某个function内。
<!--more-->
### 方式2

```javascript
test = 5;
```
这种方式隐式地声明了全局变量test，即使该语句在某个function 内。它会在这个function第一次被执行后变成全局变量。
下面的代码中，如果在不执行`testFun`的情况下，会报错；因为`a`未定义。执行了`testFun`后，`a`就成了全局变量，程序就可以正常执行。
```javascript
function testFun(){
  a = 5;
}
testFun();
console.log(a);
```

### 方式3
``` javascript
window.test = 5;
```
这种方式经常被用到一个匿名函数后将一些函数公开到全局。