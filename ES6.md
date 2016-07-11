# ES6 學習筆計
ES6 新特性
----
* let 与 const 变量宣告让变量不在被提升，让代码更逻辑化。
* 解构赋值。
* rest参数 (...变量名)，rest 参数后不可以代任何参数。  
  用于取多馀的参数放入数组。
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
* 合并数组
```
  //5
  [1,2].concat(more)
  //6
  [1,2,...more]

  var a1 = ['a','b'];
  var a2 = ['c'];
  var a3 = ['d'];

  //5
  a1.concat(a2,a3);
  //6
  [...a1,...a2,...a3]
```
* 字串转数组
```
  [...'hello']
  //['h','e','l','l','o']
```  

箭头函数 =>
----
```
var f = v => v;
等于
var f = function(v) {
  return v;
};

var f = () => 5
var f = function () { return 5; };

var sum = (s1,s2) => s1 + s2 ;
var sum = function(s1,s2) {
  return s1 + s2;
}

//若返回对向
var f = f1 => ({id:1,name:"jacky"});
```
箭头函数一个用处是简化回调函数
```
  [1,2,3].map(function (x) {
      return x * x;
  });

  [1,2,3].map(x => x * x);
```
箭头函数可以让 this 指向固定化
```
  var handler = {
    id : '123',

    init: function() {
      document.addEventListener('click',
        event => this.doS(),false);
    },

    doS: function() {
      console.log('箭头函数 callback function 指向这，而不是 window');
    }
  }

  //由于箭头函数没有自己的 this ，导致内部的 this 就是外层代码块的 this，也因
  为如此所以它不能作为构造函数。
  //除了this , arguments,super,new.target 都会指向外层
```
尾调用优化
----
此方法为函数调用时最后一步操作另一个函数，这可大大降低内存的使用，但闭包情况下还是无效。  
尾调用优化只在严格模式下开启。  
* 尾递归
递归很占内存，容易发生 stack overflow，但尾递归就不会，因为永远都只存在一个调用帧，
使用尾递归不会发生溢出，及节省内存。  
```
  //时间复杂度 O(n)
  function f1(1) {
    fi(n === 1) return 1;
    return n * factorial(n-1);
  }

  f1(5) //120

  //尾递归 O(1)
  function f1(n, total) {
    if (n === 1) return total;
    return f1(n - 1, n * total);
  }

  f1(5,1) //120
```  
对象扩展
----
允许对象中，只写属性名，不写属性值。
```
function f(x,y){
  return {x,y};
}

//等同于

function f(x,y) {
  return {x:x,y:y};
}

f(1,2) // Object {x:1,y:2}
```
方法也可以简写
```
var o = {
  method() {
    return "Hello";
  }
}

var o = {
  method: function() {
    return "Hello";
  }
}
