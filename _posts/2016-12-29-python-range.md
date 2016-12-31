---
layout: post
title: "做练习想开的"
---


###Python range


做js的练习，也算有所得，比如这个题，要求实现range(start, end, step)， step可选，再实现sum：


```
function range(start, end, step) {
    step = null || 1;
    var array = [];
    if (step > 0){
        for (var i = start; i <= end; i += step)
            array.push(i);
    } else {
        for (var i = start; i >= end; i += step)
            array.push(i);
    }
    return array;
}


function sum(array) {
    var total = 0;
    for (var i = 0; i < array.length; i++)
        total += array[i];
    return total;
}

```

所以Python的range也是这么implement的，只是Python的是小于end，而非小于等于

### reverse vs reversed

Python 的 in-place reverse是， 其实in-place reverse也就是头尾两两交换O(N)：

```
a = [1, 2, 3]

a.reverse()
a = [3,2,1]


也可以这样用
reversed(a)
// → <listreverseiterator object at 0x1006e1690>

for i in reversed(a):
	print i

// 
	3
	2
	1
a 不会变
```

reversed 是 Return a reverse iterator

类似有

- list.sort() // in place sort
- sorted(list) // 生成一个新的list








