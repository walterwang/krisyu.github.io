---
layout: post
title: iOS编程基础读书笔记第三章
---

#### 强类型

- 首先，Swift会自动推测变量/常量类型，但是Swift可能会错误推断或者不知所措（特别对于collection类型）或者为了提醒自己，都可以显式声明变量类型。
- let x: Int 绝对不是一个好的写法，因为已经遇到过各种报错了，Swift编译器会阻止你使用从未赋值过的变量。


#### 计算初始化器（ Computed Initalizer

对于使用计算初始化我一直有很大问题，然而突然开始make sense起来，因为这是应用一个匿名函数来计算赋值，因为有时候这个变量与别的相关。

```
let timed: Bool = {
	if val == 1 {
		return true
	} else {
		return false
	}
}()
```

#### 计算变量 Computed variable

先看一个例子：

```
var now: String {
    get {
        return NSDate().description
    }
    set {
        print(newValue)
    }
}

now = "Howdy" // Howdy
print(now)    // 2017-06-19 03:18:16 +0000
```
其实这里的 Howdy 根本没有被使用，我们可以省去setter让它变成一个只读变量，

```
var now: String {
	return NSDate().description
}
```

注意看以上这个只读变量，它跟初始化的区别是我们并没有括号来调用这个函数。计算变量用于以下几处：

- 只读变量
- 门面函数 （比如需要的值都是通过一个函数计算出来，那我们就把它变成一个只读的计算变量


#### Setter

这个setter特别有用和有意思

```
var s = "whatever" {
	willSet {
		print(newValue)
	} 
	didSet {
		print(oldValue)
		// self.s = "something else"
	}
}
```

之所以说它有意思是因为这个didSet是每次当设置这个值的时候就被调用。看苹果的模板都在使用它：

```
var detailItem: AnyObject? {
	didSet {
		// update the view
		self.configureView()
	}
}
```

我觉得这些算Swift的syntatic sugar吧，看一个实际使用的例子：

```
@IBOutlet weak var scrollView: UIScrollView!
    {
    didSet{
        scrollView.contentSize = imageView.frame.size
    }
}
```

#### Int & Double

就数学计算来看，Swift本身的话就是 Int 和 Double 基本上就可以完事，但可惜的是Swift并不是孤岛，我们需要和Cocoa 和各种API合作。比如画图的时候需要Float（CGFloat），比如和video duration相关的更是一些别的，比如一些从C库拿来用的一些函数。


```
sqrt(2.0) // This was expecting C double ,that is a Double, so cannot put 2
Int(arc4random()) % 256 // arc4random 返回 UInt32
```

幸好xcode很多时候会提醒我们。

#### String

常用Swift的字符串插入功能。

```
print("You have \(n) widgets.")
```

至于String转成Int因为会有失败的可能，所以得到的optional。然后这里的notes很有小意思，String的强制类型转换是字符串插值与使用print的基础，可以将任何对象转换为String，只要遵循如下三个协议之一： Streamble, CustomStringConvertible, CustomDebugStringConvertible.

然后字符串是.count而不是length，这是由于其unicode属性决定的。然后有很多String的方法其实是NSString来决定的，我们用的时候是有String被转成NSString，再被转回来。

有意思的比如看这里：

```
let s = "hello world"

let range = s.range(of: "ell") // optional range
let range2 = (s as NSString).range(of: "ell")  // NSRange
```


#### Character

针对一个字符串，我们可以用 s.characters 取得它的字符序列。字符序列因为是一个CollectionType，所以有很多方法可以调用。

但是有一种吓人的感觉

```
let firstL = s.characters.index(of: "l")
print(firstL)
// Optional(Swift.String.CharacterView.Index(_base: Swift.String.UnicodeScalarView.Index(_position: 2), _countUTF16: 1))
```

check 是否存在元音：

```
let s = s.chracters.contains { "aeiou".characters.contains($0) }
```

反正collectiontype就尽情的跟map，filter结合起来写一些迷惑的代码。

另外，如果想用角标来寻求某个字符基本很难，因为String的索引是String.CharacterView.Index 这种嵌套类型，看起来就 abstruse。另外一种做法是吧数组转换成Character 对象数组，操作完毕再转换回来。

但是发现so很多回答提供 Extension 来做这件事

[Get nth character of a string in Swift programming language](https://stackoverflow.com/questions/24092884/get-nth-character-of-a-string-in-swift-programming-language)

#### Range

没有想到的用处

```
let d = 0.35555

if (0.1...0.9).contains(d) //
```

声明： 以上的Int， Double， String， Character , Range 都是结构体。

#### 元组

原来使用元组可以实现变量值的互换，in a Pythonize way.

#### Optional

Optional 是枚举，refresh 了两个点，一个是我们用optional链得到的也是optional,第二是即使optional，我们也可以直接比较。例子都如下：

```
let s: String? = "Kris"
let upper = s?.uppercased()
// upper is optional upper case

if s == "Kris" {
    print("true")
}
// true
```
