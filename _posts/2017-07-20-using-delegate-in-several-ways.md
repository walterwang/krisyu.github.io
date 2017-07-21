---
layout: post
title: "使用delegate的几种姿态"
---

delegate是protocol的一种，我们遵循这个协议就需要实现protocol中的一些方法。最早接触delegate是 UITableViewController，controller是tableview的代理，里面来写一些方法来控制tableview的row的行为或者外观。


### 姿态一

传统的这个类遵循这个协议，然后我们把它写在这遵循之后，在这个class里面实现方法。

```
class XViewController: UITableViewController, UITableViewDelegate {
	...
} 
```

### 姿态二

因为有了extension，所以有时候你发现你的协议被放到另一个地方去了

```
extension XViewController: UITableViewDelegate {
	...
}
```

### 姿态三

比如在这个[app例子中](https://github.com/KrisYu/swift14macOSApps/tree/master/08-Puzzle):

1. 声明协议 PuzzleDataSource，有方法 cellsForPuzzle
2. puzzleWindow 遵循PuzzleDataSource协议，实现方法
3. 去puzzleView定义 open var dataSource: PuzzleDataSource? 并且使用这个变量
4. 回到 puzzleWindow中使用puzzleView，并且让它的datasource 为puzzleWindow

这样也是棒棒的，real•体现delegate，体现•真•委托精神。