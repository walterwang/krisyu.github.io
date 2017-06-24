---
layout: post
title: "External Parameter和Init"
---

### External Parameter

事实证明，这个好像比我想象的更有用一些。

```
func join(string s1: String, toString s2: String, withJoiner joiner: String) -> String {
    return s1 + joiner + s2
}
```

比直接放三个string 作为parameter就好很多。

参见 SO 的答案


[External Parameters in Swift](http://stackoverflow.com/questions/28161383/external-parameters-in-swift)

[What is the difference between Local and External Parameter Names in Swift](http://stackoverflow.com/questions/27934253/what-is-the-difference-between-local-and-external-parameter-names-in-swift)



### init()

> 类和结构体在创建实例时，必须为所有存储型属性设置合适的初始值。存储型属性的值不能处于一个未知的状态。


[构造过程](https://znoodl.gitbooks.io/swift/content/chapter2/14_Initialization.html)

这也是我们写 ViewController 的时候写一个存储属性就一定要给它赋值的原因，甚至ViewDidLoad 中放都不行，我们可以放在 init中


> 然而，构造器并不像函数和方法那样在括号前有一个可辨别的名字。因此在调用构造器时，主要通过构造器中的参数名和类型来确定应该被调用的构造器。正因为参数如此重要，如果你在定义构造器时没有提供参数的外部名字，Swift 会为构造器的每个参数自动生成一个跟内部名字相同的外部名。

如果需要避免外部名字则需要添加 _ 

然后再度发现结构体如果给了默认值可以不用写构造器,如下也👌

```
struct Size {
    var width = 0.0, height = 0.0
}
let twoByTwo = Size(width: 2.0, height: 2.0)
```


### init vs convenience init

指定构造器和便利构造器,只是简单的加不加 convenience 的区别。再来几个required 再加上 init(coder aDecoder: NSCoder) 简直可以更晕了， 因为subclass之类的有时候写起来init或者读别人的代码简直感觉是盲人摸象。

感觉这篇文章关于[类的构造器继承啥的](https://znoodl.gitbooks.io/swift/content/chapter2/14_Initialization.html#class_inheritance_and_initialization)的可以够读十天了|||
 
