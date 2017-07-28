---
layout: post
title: "如何阅读Swift源码"
---

写给知乎某问题的，也mark一下自己的缺失。


## 在哪读

### 在本地读

可以参见这篇文章- [如何阅读 Swift 标准库中的源码](http://swift.gg/2016/12/30/how-to-read-the-swift-standard-libray-source/)，原文有英文链接，这样是编译之后在本地读，不过请准备好硬盘空间和稍等时间耐心编译。


### 直接在Github读

link -> <https://github.com/apple/swift>
 
 
## 怎么读

的确是要带有目的的读，然而怎么带目的呢？推荐先从这个core文件夹开始-> <https://github.com/apple/swift/tree/master/stdlib/public/core>

### 例子一

Optional 这个是入 Swift 必知的东西，所以我们来看一下Optional， Optional 就是enum，两个状况, 要么nil，要么something，至于some(Wrapped)，some的状况就是关联值为Wrapped

```
@_fixed_layout
public enum Optional<Wrapped> : ExpressibleByNilLiteral {
  // The compiler has special knowledge of Optional<Wrapped>, including the fact
  // that it is an `enum` with cases named `none` and `some`.

  /// The absence of a value.
  ///
  /// In code, the absence of a value is typically written using the `nil`
  /// literal rather than the explicit `.none` enumeration case.
  case none

  /// The presence of a value, stored as `Wrapped`.
  case some(Wrapped)

  /// Creates an instance that stores the given value.
  @_transparent
  public init(_ some: Wrapped) { self = .some(some) }
  
  ...
  
 }
```

### 例子二

比如我们打开 Algorithm.swift，直接看第一个函数，求最小值的函数，非常简单和清晰，不过也有知识点（泛型函数，使用_来避免函数参数的外部名）：

```
/// Returns the lesser of two comparable values.
///
/// - Parameters:
///   - x: A value to compare.
///   - y: Another value to compare.
/// - Returns: The lesser of `x` and `y`. If `x` is equal to `y`, returns `x`.
@_inlineable
public func min<T : Comparable>(_ x: T, _ y: T) -> T {
  // In case `x == y` we pick `x`.
  // This preserves any pre-existing order in case `T` has identity,
  // which is important for e.g. the stability of sorting algorithms.
  // `(min(x, y), max(x, y))` should return `(x, y)` in case `x == y`.
  return y < x ? y : x
}
```

@_inlineable修饰符对我来说也很新。


### 例子三

假设我看到这一段代码，觉得这个filter很厉害啊，向更加了解它，[filter](https://developer.apple.com/documentation/swift/sequence/2905694-filter)

```
let cast = ["Vivien", "Marlon", "Kim", "Karl"]
let shortNames = cast.filter { $0.count < 5 }  // swift 4.0
// let shortNames = cast.filter { $0.characters.count < 5 } swift 3.0
print(shortNames)
// Prints "["Kim", "Karl"]"
```

进 Sequence.swift 文件查看，原来filter的函数定义是这样:

```
  @_inlineable
  public func filter(
    _ isIncluded: (Element) throws -> Bool
  ) rethrows -> [Element] {
    return try _filter(isIncluded)
  }

  @_transparent
  public func _filter(
    _ isIncluded: (Element) throws -> Bool
  ) rethrows -> [Element] {

    var result = ContiguousArray<Element>()

    var iterator = self.makeIterator()

    while let element = iterator.next() {
      if try isIncluded(element) {
        result.append(element)
      }
    }

    return Array(result)
  }
```

这里的 isIncluded的类型是 Element -> Bool，filter的最终返回类型是 [Element]，都很make sense，当然还包含更多的错误处理，throw 和 rethrow， try，错误处理这个部分我自己也需要加强

然后发现仅仅读 comments 部分都能学到一些新知识，比如 for in 用的是 iterator，还看到了一些之前从没用过的（但是肯定能增加效率的）函数。

Sequence protocol 其实很有意思，很多函数都是息息相关，我记得我扫过某本js书的开头，介绍四大函数 : forEach, map, reduce, filter, Swift也有这四个，还有更多， 比如 dorp(while: ), contains(where:) ...



## 读的进阶

读的进阶我们可以尝试一些练习，比如读完 filter 我们可以尝试写一个 count(:where), 不新建数组，仅仅计算满足条件的元素个数。




