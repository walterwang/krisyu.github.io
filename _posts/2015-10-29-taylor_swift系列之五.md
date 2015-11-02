#Taylor Swift系列之五

###UIView

首先这里与之前不同的地方是我们自行添加了一个UIView - rate star，这个rate star自成一体，有自己的control和view，它的view居住在Main.Storyboard之内，但是它的control则是自己的swift文件。

首先我们做的是创建了一个iOS的Cocoa Touch Class，然后让它变成UIView的subclass，给之命名为RatingControl,其实也就是创建了一个RatingControl.swift文件，我们将会用这个文件来初始化，和控制最终实现评分机制....


>You typically create a view in one of two ways: by initializing the view with a frame so that you can manually add the view to your UI, or by allowing the view to be loaded by the storyboard. There’s a corresponding initializer for each approach: init(frame:) for the frame and init?(coder:) for the storyboard.

这里用的是 init?(coder:)方法，因为这里是要和storyboard联起来。

```
required init?(coder aDecoder: NSCoder) {
    super.init(coder: aDecoder)
}

```

然后添加UIView之后，然后再跟这个control（.swift file）联系起来.
//Intrinsic Size（intrinsicContentSize）出现了好多次，目前存疑


```
required init?(coder aDecoder: NSCoder) {
    super.init(coder: aDecoder)
    
    let button = UIButton(frame: CGRect(x: 0, y: 0, width: 44, height: 44))
    button.backgroundColor = UIColor.redColor()
    addSubview(button)
}
```

这里使用代码来添加了一个UIButton 常量.


###分号悲剧


这里学到了新的方法给button添加action，值得注意的是Swift的方法名是ratingButtonTapped(_:),有“引号”，如果没有添加引号就会报错悲剧.....


```
button.addTarget(self, action: "ratingButtonTapped:", forControlEvents: .TouchDown)
```

然后把一个button变成一组button用的方法

```
var ratingButtons = [UIButton]()

```

然后用for in把之前的let button等括起来，就可以创建一组了，注意创建一组之后需要再使用layoutSubviews来分散分布buttons




### Button Action

// to be understand, 暂时感觉是非常精妙和稍显难以理解



