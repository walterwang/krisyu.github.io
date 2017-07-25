---
layout: post
title: "init(coder:)错误到底为啥？"
---


很多时候在ViewController里会碰到的错误提醒："fatal error: use of unimplemented initializer 'init(coder:)' for class"。在今天，终于搞懂原因了，先看这个例子:

(在Terminal里运行Swift再简单不过了，直接type swift，于是我们就到了命令行界面.)

```
  1> protocol Flier { init() }
  2> class Bird: Flier { init(){} }
error: repl.swift:2:21: error: initializer requirement 'init()' can only be satisfied by a `required` initializer in non-final class 'Bird'
class Bird: Flier { init(){} }
                    ^
                    required 
                    
```

两种修改方式，要么将Bird标记成final，要么改成required init.

这是因为如果协议声明了一个初始化器，同时一个类使用了这个协议，那么这个类就必定要实现这个初始化器。

ViewController报这个错误是因为 UIViewController 使用了协议 NSCoding，如果不使用自己的init就还好，但是一旦使用了自己的init就需要初始化器 init(coder: )，基本上我们添加一句占位符就可以解决，里面也可以写成fatalError啥的，个人理解相当于占位符。


```
required init?(coder aDecoder: NSCoder) {
    super.init(coder: aDecoder)
}
```

SO上有很多清楚的解答：

[Fatal error: use of unimplemented initializer 'init(coder:)' for class](https://stackoverflow.com/questions/24036393/fatal-error-use-of-unimplemented-initializer-initcoder-for-class)

[What exactly is init coder aDecoder?](https://stackoverflow.com/questions/38386339/what-exactly-is-init-coder-adecoder)