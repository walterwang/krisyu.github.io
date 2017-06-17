---
layout: post
title: "Swift中的@escaping"
---


要理解@escaping，首先需要理解closure， 要理解closure，首先理解匿名函数。
 

### 先理解匿名函数

要在Swift中构造匿名函数，需要：

1. 创建函数体，包括花括号，但是不需要函数声明
2. 如果必要，将函数的参数列表与返回类型作为花括号中的第一行，后跟关键字in.

例子1： 将以下函数变成匿名函数：

```
func whatToAnimate(){
	self.myButton.frame.origin.y += 20
}
```

匿名函数版本：

```
{
	() -> () in
	self.myButton.frame.origin.y += 20
}
```

例子2： 有参数的具名函数：

```
func whatToDoLater(finished: Bool){
	print("finished: \(finished)")
}
```

匿名函数版本：


```
{
	(finished: Bool) -> () in
	print("finished: \(finished)")
}
```

可省略的地方：

1. 省略返回类型
2. 没有参数可以省略 in 这一样
3. 省略参数类型
4. 省略圆括号，这个是如果就一个参数，并且我们编译器可以推断出其类型的话
5. 省略 in， 直接用名字比如 $0
6. 省略参数名，用_代替
7. 省略函数实参标签（又叫尾函数
...

一路省略下来，匿名函数真是节约。

### 再理解闭包

理解匿名函数之后，我们来看闭包的表达式：

```
{ (parameters) -> return type in
    statements
}
```

这就是匿名函数啊，而我们叫它闭包则是因为：

> 闭包可以捕获和存储其所在上下文中任意常量和变量的引用。 这就是所谓的闭合并包裹着这些常量和变量，俗称闭包。

而在这一篇中，我们可以一步一步看到如何从


```
reversed = sorted(names, { (s1: String, s2: String) -> Bool in
    return s1 > s2
})
```

利用省略到：

```
reversed = sorted(names, >)
```

再利用 trailling closure的特性，可以这样：

```
reversed = sorted(names) { $0 > $1 }
```

闭包当然还有更好的例子，因为我们来看它的一些特性。

### Escaping Closure（逃逸闭包


> 如果一个闭包被作为一个参数传递给一个函数，并且在函数return之后才被唤起执行，那么这个闭包是逃逸闭包。

好抽象的描述，这篇文章写得不错：

不逃逸闭包的生命周期：

1. Pass a closure into a function
2. The function runs the closure (or not)
3. The function returns

然后这个closure就死掉了。

而逃逸闭包则会一直存在，没有因为function被kill而死掉，所以我们叫这个闭包为逃逸闭包（？

在以下的两种情况，我们需要使用 escaping closure：

1. 异步execution，并不能说函数return了就把closure kill掉，因为这个closure可能还没有执行完毕
2. 存储，如果任何全局变量都有一些些存储存在，那么这个closure也被逃逸掉了。

在 Swift 1 和 2中， closure by default 是 escaping的，所以我们需要用 @noescape 来mark.
在 Swift 3中，closure by default是non-escaping，我们需要用@escaping 来mark



> In Swift 3, closure parameters are non-escaping by default; you can use the new @escaping attribute if this isn’t what you want. Non-escaping closures passed in as arguments are guaranteed to not stick around once the function returns.

而一般情况下，弱🐔就跟着Xcode的提示走？



参考：

1. \<iOS 9 Programming Fundamentals with Swift> by Matt Neuburg
2. [闭包](https://numbbbbb.gitbooks.io/-the-swift-programming-language-/content/chapter2/07_Closures.html)
3. [Escaping and Nonescaping Closures in Swift 3](https://swiftunboxed.com/lang/closures-escaping-noescape-swift3/)