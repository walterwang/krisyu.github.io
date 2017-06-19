---
layout: post
title: iOS编程基础读书笔记第二章
---


#### 返回类型与参数

值得注意的是，不同于别的语言，我们是把参数类型放在参数后面，然后返回值很容易理解

```
func say1(s: String) -> Void { print(s) }
```

返回Void也可以忽略或者写成括号。

#### 函数签名

`（Int, Int） -> Int` 叫函数签名


#### 外部参数名

一开始有点不解为什么我们需要外部参数名，但是突然开始认识到它的好。

```
func repeatString(s: String, times n: Int) -> String{
	var result = ""
	for _ in 1...n { result += s }
	return result
}
```

这样调用的时候我们就使用times，而与n无关。

```

let s = "hello"
let s2 = s.replacingOccurrences(of: "ell", with: "ipp")
// s2 is now "hippo"
```

这样觉得要清晰很多，当然如果你不喜欢也可以阻止参数外化，比如这样：

```
func sum(_ x:Int, _ y: Int) -> Int

// sum(a,b) to call 
// otherwise we have to write sum(x: a, y: b) 
```

Notice: In Swift 3.1, 我觉得下划线并不是一个很好地选择，我觉得let it be就很不错。
 


#### 默认参数值

跟Python等类似，我们可以直接给默认参数

```
func sum(x: Int, y: Int = 5) -> Int{
    return x + y
}

sum(x: 3, y: 4)
// 7
sum(x: 3)
// 8
```

#### 可变参数（这个应该翻译成数组参数吧

话说我从来还没有注意过参数后面加省略号的，原来是应该理解成数组参数。

```
func sayStrings(arrayOfString: String ...){
    for s in arrayOfString {
        print(s)
    }
}

print("hey", "how", "are", "you")
// hey how are you
```


#### 可修改参数

这个是一开始Swift真心让我震惊的地方，好吧，其实跟C什么的相比也还好（？）。

> 在函数体中，参数本质上是个局部变量。在默认情况下，它是个隐式是用let声明的变量。你无法对其赋值。


实际上当我想尝试写

```
func removeFromString(var s: String, character c: Character) 
```

它就给我报错，推荐我使用一个本地copy。

实际上最终是写成这样的：

```
func removeFromString(s: inout String, character c: Character) 

removeFromString(s: &s, character: Character("l"))
```

调用的时候也是用了地址。然后s一定要是一个var.

但是，如果我们来看这个例子：


```
class Dog {
    var name = ""
}

func changeNameOfDog(d: Dog, to: String){
    d.name = to
}

let d = Dog()
d.name = "Fido"
print(d.name) // "Fido"
changeNameOfDog(d: d, to: "Rover")
print(d.name) // "Rover"
```

这是因为类是引用类型，而其他对象类型风格则是值类型（pass by reference or pass by value）

PS: inout 等同于 ObjC 中的 UnsafeMutablePointer.


#### 一等公民函数

函数是一等公民，这件事其实也不太用强调，对我们来说怎么更好的使用这个特性是重点。
 


然后要学着看懂各种函数的省略形式。可以参见一部分[Swift中的@escaping](http://krisyu.github.io/2017/06/03/swift-escaping-meaning.html)

其实闭包的‘闭’ capture之特性可以在各种地方看到，而我们需要明了的是我们有那么多self出现这完全也是闭包的功劳，如果没有闭包，我们根本就没法达到不属于它的作用域，就没法完美控制。有那么多pass in closure的函数就没法完啊。

另外，闭包的一些捕获和修改功能有点震惊（像Java里面的类static变量？），比如如下的例子（应该是来自官方），也是蛮令人惊讶的。

```
import UIKit

func makeIncrementor(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementor() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementor
}

let incrementByTen = makeIncrementor(forIncrement: 10)

incrementByTen()
incrementByTen()
incrementByTen()
```

#### 柯里化函数 （Currying Function

柯里化函数就是原本我们这样，如果函数返回的函数接受一个参数,那么我们可以便捷的写成另外一种方式，做一些省略。


```
func makeRoundedRectangleMaker(sz: CGSize) -> (CGFloat) -> UIImage {
    return {
        r in
        imageOfSize(size: sz) {
            let p = UIBezierPath.init(roundedRect: CGRect.init(origin: .zero, size: sz), cornerRadius: r)
            p.stroke()
        }
    }
}

// makeRoundedRectangleMaker(sz: CGSize.init(width: 45, height: 30))(8)



func makeRoundedRectangleMaker(sz: CGSize, r: CGFloat) -> UIImage {
    
    return imageOfSize(size: sz) {
        let p = UIBezierPath.init(roundedRect: CGRect.init(origin: .zero, size: sz), cornerRadius: r)
        p.stroke()
    }
}

// makeRoundedRectangleMaker(sz: CGSize.init(width: 45, height: 30), r: 8)
