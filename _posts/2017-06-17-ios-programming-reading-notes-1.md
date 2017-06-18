---
layout: post
title: iOS编程基础读书笔记第一章
---

#### 对象 vs 消息

说起来很高端，其实对象和消息就是`fido.bark()`， `fido`是对象，而我们向其发送的消息就是`.bark()`.说法可以是

| send the bark message, with no parameters to fido

在Swift中，万物皆对象。我们先定义一下，对象指的是你可以向其发送消息的某个实体。

一个有趣的看法是我们可以给 Int, String, Double...etc 添加Extension，这样就可以对其发送消息

```
extension Int {
    func sayHello() {
        print("Hello, I'm \(self)")
    }
}
1.sayHello() // outputs: "Hello, I'm 1"
```

然后这里的1是struct，Swift中有三种对象类型： 类、结构体与枚举。

- PS ： 感觉类和结构体经常可以混用
- PSS ： Swift的枚举非常牛逼，可以添加函数
- PSSS ： Extension真是非常厉害的，比如看stackoverflow上的很多用Swift Extension做匪夷所思的事，比如github上专用Swift Extension相关repo

#### 变量类型

Swift只是可以推断变量类型，但是它并不像JS这么灵活可以把一个原本赋值为int的变量变成string。

```
var two = 2
two = "hello" // compile error
```


#### 文件结构

- import语句
- 变量声明： 全局变量
- 函数声明： 全局函数
- 对象类型 类，结构体，枚举

一般来说（除Utilities外）一个文件里面就放一个类或者结构，不过我也其实有见过放很多对象类型的。


其它的一些topic也是一些比较常见的，比如作用域，生命周期，如何设计类型与API，这种都只能多看多联系吧。



