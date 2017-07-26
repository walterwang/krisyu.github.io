---
layout: post
title: "到底啥是柯里化(Currying)"
---


个人理解就是把函数的返回值变成一个函数？看到这篇文章：

```
func add(_ num: Int) -> (Int) -> Int {
    return { val in
        return num + val
    }
}

let addTwo = add(2)  // (Int) -> Int  
let result = addTwo(6) // 8
```

大神的总结：

> 把接受多个参数的方法进行一些变形，使其更加灵活的方法。


然后倘若我们要 addFour 直接就是 add(4), addTwo 是一个函数类型，接受Int，返回Int.看了一个[举例的应用场景](https://oleb.net/blog/2014/07/swift-instance-methods-curried-functions/?utm_campaign=iOS_Dev_Weekly_Issue_157&utm_medium=email&utm_source=iOS%252BDev%252BWeekly)，即使看了这个post还是有点疑惑到底要怎么用。

SO的这个问题也不错 [What is 'Currying'?](https://stackoverflow.com/questions/36314/what-is-currying?rq=1),然后看到原来最早（Swift 2.x）的时候也可以像js那样写curry function（说的我好像会一样），总之mark一下这个功能。


