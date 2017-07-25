---
layout: post
title: "Swift中的weak到底干啥"
---

继续读书笔记，Swift的内存管理是自动进行的，一般来说不用我们动手管理，可能会出问题的地方在于如果出现循环引用，看书上的例子：

```
func testRetainCycle(){
    class Dog{
        deinit {
            print("farawall from Dog")
        }
    }
    class Cat{
        deinit {
            print("farewall from Cat")
        }
    }
    let d = Dog()
    let c = Cat()
}

testRetainCycle() //farewall from Cat, farawall from Dog
```

如果我们做以下改变，那么console不再会有输出，实际上说明我们的这个c和d没有被deinit，原因是Dog和Cat对象互相引用，并且会是强引用，内存泄露就此造成：

```
func testRetainCycle(){
    class Dog{
        var cat: Cat?
        deinit {
            print("farawall from Dog")
        }
    }
    class Cat{
        var dog: Dog?
        deinit {
            print("farewall from Cat")
        }
    }
    let d = Dog()
    let c = Cat()
    d.cat = c
    c.dog = d
}

testRetainCycle() // nothing in console
```

解决方案就是把其中一个声明为weak类型，比如 class Dog 里面写成 weak var cat，当然这是非常非常简单的例子，突然感觉到了一阵害怕，不知道以前自己是不是犯过这种错，在别人的代码里翻看了一下使用weak的例子，closure，突然一阵惊慌😱