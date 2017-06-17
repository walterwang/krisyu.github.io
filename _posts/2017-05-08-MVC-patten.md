---
layout: post
title: "MVC 梳理"
---


看到了一个so回答的不错，这样来看mvc：

- model,如果完全没有UI，你的游戏/程序是怎么样的，比如写Python，一开始就写那种terminal里面的ascii游戏
- view,仅仅负责画东西
- controller，控制

感觉需要重看cs 193p的lecture 2.这样就来了很多问题，model的数据要怎么告诉view，view被点击了，数据改变了如何告诉model，这一切都是controller来管。


### model -> controller -> view传递数据

所以对iOS来说，dataSource和delegate就出现了， **a real MVC app**, 在controller中，我们定义model，然后把数据传给view,这个可以通过以下方式来做到，我们可以写一个dataSource的协议，然后让controller实现这个协议，而在相应的model中我们声明和获得这些东西：

```
// In View
var numbers: [[String]] {
    return dataSource!.numbersForPuzzle()
}
    
open var dataSource: PuzzleDataSource?


// In Controller
protocol PuzzleDataSource {
    func numbersForPuzzle() -> [[String]]
}

extension ViewController: PuzzleDataSource{
    func numbersForPuzzle() -> [[String]] {
        return self.model.numbersForPuzzle()
    }
}
    
```

### view -> controller -> model 数据更新

然后当我们来更新view的时候，比如我们点击view可能需要更新model中的数据，这个时候我们让controller来当view的delegate.


可以把所有相关的处理放在controller中，或者甚至放在model中，只要让这个是它的delegate就行。

我们可以这样做：


```
// In View
open var delegate: PuzzleDelegate?
```

然后有相应的处理方法，只是这个处理方法我们调用的的是 delegate?.handleMethod()


```
// In controller

protocol PuzzleDelegate {
    func touch(at tile: Tile)
}

extension PuzzleVC: PuzzleDelegate{
}
```

在这个相应的controller的 touch at方法中，我们就可以尽情的使用model,更新view.

### 一些别的

Swift 的 initializer 实在太多了， 需要花点时间来理一理， 在思考UIViewController的 init，因为它的viewDidLoad其实可以更多放跟UI相关的东西，发现可以写在init(coder:)里面

比如：

```
required init?(coder aDecoder: NSCoder) {
	 // init property or others
    super.init(coder: aDecoder)
}
```


关于MVC: <https://developer.apple.com/library/content/documentation/General/Conceptual/DevPedia-CocoaCore/MVC.html>
