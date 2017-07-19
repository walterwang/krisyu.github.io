---
layout: post
title: "枚举，结构体与类"
---

## pass by value/reference

swift中的enum/struct 算蛮强大的，特别struct，有时候我都会疑惑struct 还是 class，感觉之前写的一些class都可以是struct,比如之前那篇log system，当然class有的特性更多/更强大。

而 struct/enum 与 class 的一个明显区别就是pass by value/reference, show me the code:

```
struct Digit {
    var number: Int
    init(_ n: Int) {
        self.number = n
    }
}


var d = Digit(123) {
    didSet{
        print("d was set")
    }
}

d.number = 42  // d was set print in console 
```

所以实际上我们来改变 d.number 其实也就是换了一个新的Digit来替换之前的，而在struct之内的要修改其本身实例方法的需要标记为 mutating，这个我已经见识过了。并且之上的d只能被定义为var.

看一下类：

```
class Dog {
    var name: String = "Fido"
}

var rover = Dog() {
    didSet{
        print("did set rover")
    }
}

rover.name = "Rover" // no output in console
```

另一个可以看得是：

```

var d = Digit(123)
print(d.number)
var d2 = d
d2.number = 42
print(d.number)

var fido = Dog()
print(fido.name)
var rover = fido
rover.name = "Rover"
print(fido.name)
```

在对枚举或结构体实例赋值时候，实际上会执行复制，创造出全新的实例。不过在对类进行赋值时，得到的是对相同实例的新引用。

参数传递也是这样，struct/enum传入的本质上还是let，并不会影响传入的struct/enum，甚至对array都是这样，而class则会改变，因为传入的是引用。

## 子类/父类

比如 `class ViewController: UIViewController`，方法都被继承下来，直接调用，还可以override， self 和 super的关系。

而正因为类更强大的继承，类的初始化就更加复杂。

