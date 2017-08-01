---
layout: post
title: "swift中的泛型"
---

继续我的读书笔记，书里面提到了四中可以声明Swift泛型的例子，不过看到最常见的还是泛型函数和泛型对象类型，比如随便打开大名鼎鼎的 [swift-algorithm-club](https://github.com/raywenderlich/swift-algorithm-club) 看Stack，使用泛型：

```
public struct Stack<T> {
  fileprivate var array = [T]()

  public var isEmpty: Bool {
    return array.isEmpty
  }

  public var count: Int {
    return array.count
  }

  public mutating func push(_ element: T) {
    array.append(element)
  }

  public mutating func pop() -> T? {
    return array.popLast()
  }

  public var top: T? {
    return array.last
  }
}
```


再随意看一个 insertion sort的函数：

```
func insertionSort<T>(_ array: [T], _ isOrderedBefore: (T, T) -> Bool) -> [T] {
	// ...	
}
```


书里还有一个有趣的例子，某种程度上也解释了为什么 insertionSort 为什么是这么写的，如果我们直接写一个这样的函数：

```
func myMin<T>(things: T ...) -> T {
    var minimum = things[0]
    for ix in 1..<things.count {
        if things[ix] < minimum { // compile error
            minimum = things[ix]
        }
    }
    return minimum
}
```
其实也很容易理解为啥会报错，这个things 不一定知道如何比大小，所以一个解决方案是让这个T遵循 Comparable 协议， 直接修改函数

```
func myMin<T: Comparable>(things: T ...) -> T  
```

即可解决。

调用看结果

```
 38> myMin(things: 1,2,3,4,5,8,7,9,-1)
$R1: Int = -1

```

