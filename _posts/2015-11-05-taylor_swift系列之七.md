#Taylor Swift系列之七

### Data Model Class

这里import UIKit 而非 import Foundation,然后Swift的class写起来和别的语言的class写起来基本一致，然后这里的class也和Int，UIImage一样，可以是optional的...

给init方法加一个问号就能解决问题，就能变成optional，变成optional是用于控制，比如如果初始化值是不被允许，那么就return nil...

测试的时候用的是XCTest类，测试方法看起来也不那么难，用的XCTAssertNil(),XCTAssertNotNil()等方法，也和Python assert类似...


###UITableView

UITableView绝对属于各方爱讲和重点，之前也随手[记录过][id],然后这里建了好几个类，首先是MealTableViewCell，它是用来自定义TableViewCell这个类的，所以它是UITableViewCell的子类.

[id]:http://krisyu.github.io/2015/UITableViewController记录一点/



意思就是，这个类，它是控制一个cell是如何表示的，注意的是这里的Rating依旧用的是View Object，然后用的是RatingControl这个class（？）

然后同样，在MealTableViewCell.swift里面把这些元素全部定义一次，联系起来。


再出现了第二个类MealTableViewController，是UITableViewController的子类，
在MealTableViewController创建了mutable array meals，然后用了一些sample data，但直到现在我们都没有展示出来数据：

```
var meals = [Meals]()
```

###Display the data

这里又出现了： delegate 和 data source，在之前的随手记和各种里面也有出现关于delegate的些许笔记.真是不得不学会啊......

惊讶之处在于把cell downcast成为MealTableViewCell，然后依旧晕晕的。


```
let cell = tableView.dequeueReusableCellWithIdentifier(cellIdentifier, forIndexPath: indexPath) as! MealTableViewCell
```