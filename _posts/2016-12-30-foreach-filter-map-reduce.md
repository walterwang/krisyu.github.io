---
layout: post
title: "forEach, filter, map, reduce"
---

感觉这四个函数是一霸，非常厉害


### forEach

本体

```
function forEach(array, action) {
  for (var i = 0; i < array.length; i++) {
    action(array[i]);
  }
}

forEach(["Wampeter", "Foma", "Granfalloon"], console.log);
```

实际js中写法：

```
// the real way of writing in js
var numbers = [1,2,3,4,5], sum = 0;
numbers.forEach(function(number){
  sum += number;
});

console.log(sum);

```

因为这四个都是Array的method。 Python中没有对应的for Each，就只能用本体写法^_^


### filter

本体

```
function filter(array, test) {
  var passed = [];
  for (var i = 0; i < array.length; i++) {
    if (test(array[i]))
      passed.push(array[i]);
  }
  return passed;
}
```

js写法：


```
var numbers = [1,2,3,4,5];

function isEven(value) {
  return value % 2 == 0;
}
console.log(numbers.filter(isEven));

// 这样也ok
numbers.filter(function(value){
  return value % 2 == 0;
});
```

python 用法，写法，比如这个例子：

Replace all non-alphanumeric characters in a string


```
s = 'abcdjiyiuy**&&#$%^&*(1234567890'
s = filter(str.isalnum, s)
s → 'abcdjiyiuy1234567890'
```

前面放一个函数来filter


发现了这篇文章和这本小书<http://book.pythontips.com/en/latest/map_filter.html>


### map

本体

>The map() method creates a new array with the results of calling a provided function on every element in this array.

forEach强调对于array里面的每个element做action,而map则是return一个新的array.


```
function map(array, transform){
  var mapped = [];
  for (var i = 0; i < array.length; i++) 
    mapped.push(transform(array[i]));
  return mappped;
}
```


js例子

```
var numbers = [1, 5, 10, 15];

var roots = numbers.map(function(x){
  return x * 2;
});

roots
→ [2, 10, 20, 30] 
```


例子来自于<https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference>


### reduce

本体

```
function reduce(array, combine, start) {
  var current = start;
  for (var i = 0; i < array.length; i++)
    current = combine(current, array[i]);
  return current;
}

console.log(reduce([1, 2, 3, 4], function(a, b) {
  return a + b;
}, 0));
```

js写法

```
var sum = [0, 1, 2, 3].reduce(function(a, b) {
  return a + b;
}, 0);
```

原来reduce还有这么棒的一个地方：

> The standard array method reduce, which of course corresponds to this function, has an added convenience. If your array contains at least one element, you are allowed to leave off the start argument. The method will take the first element of the array as its start value and start reducing at the second element.

### 结合起来的力量

把这四个结合起来用的例子，注意这里js的`+`并不是一个function，不是value，所以只得自己定义一个plus函数。

但是总得看起来还是非常便利。


```
function average(array) {
  function plus(a, b) { return a + b;}
  return array.reduce(plus) / array.length;
}

function age(p){ return p.died - p.born; }
function male(p) { return p.sex == 'm'; }
function female(p) { return p.sex == 'f';}


console.log(average(ancestry.filter(male).map(age)));
console.log(average(ancestry.filter(female).map(age)));
```