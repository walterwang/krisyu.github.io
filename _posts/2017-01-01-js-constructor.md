---
layout: post
title: "JS创建Object"
---

### Constructor

原来JS的Constructor是这样的，一个function配一个new就行。


### Call 和 Apply

原来还可以这样用

```
console.log(Object.prototype.toString.call([1, 2]));
console.log(Array.prototype.toString.apply([1, 2]));
```