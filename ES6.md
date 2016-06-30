# ES6 學習筆計
ES6 新特性
----
* let 与 const 变量宣告让变量不在被提升，让代码更逻辑化。
* 解构赋值。
* rest参数 (...变量名)，rest 参数后不可以代任何参数。  
```
  function f (a,...b,c) {} //报错
```
* spread 是三个点(...), 将数组转为参数序列。
```
  //ES5
  function f(x,y,x) {
    //..
  }
  var args = [0,1,2];
  f.apply(null,args);

  //ES6
  function f(x,y,x) {
    //..
  }
  var args = [0,1,2];
  f(...args);

  //Math.max
  //ES5
  Math.max.apply(null,[14,3,7]);
  //ES6
  Math.max(...[14,3,7]);

  //push
  //ES5
  var arr1 = [1,2,3];
  var arr2 = [3,4,5];
  arr1.push(...arr2);
```
