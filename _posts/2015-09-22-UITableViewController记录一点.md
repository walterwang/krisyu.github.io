#UITableViewController

###一般的ViewController


一般的ViewController + Table View也可以做table view（这句话感觉好别扭），但是需要手动的连接delegate 和 datasource，不如直接使用TableViewController来的方便。

各种control drag



然后最重要的两个方法如下：


```
• tableView(_:numberOfRowsInSection:)

• tableView(_:cellForRowAtIndexPath:)


```




###Custom Cell



一般的Cell也是可以直接自带image的，key code：



```

cell.imageView?.image = UIImage(named: "restaurant")

```

但是如果要cell更好看，那么记得需要把Cell的类型由 Basic 改成 Custom，然后在Table View里做各种更改，在Cell里做各种更改，然后拖拽各种想放的比如Label，Image...

然后要Creating a Class for the Custom Cell，同样记得去改对应的Class

同样，如果想要把方形图片变成圆角可以用code


```

￼cell.thumbnailImageView.layer.cornerRadius = cell.thumbnailImageView.frame.size.width / 2

//cell.thumbnailImageView.layer.cornerRadius = 10.0cell.thumbnailImageView.clipsToBounds = true

```

可以各种尝试各种改，虽然帮助文档半看不懂状态，但是随手改的好处是随便run一下就能看到结果


###DataSource 和 Delegate


DataSource是数据来源

Delegate则是处理一些相关动作的，比如选中某行


所以一个重要的方法再度出现


```

tableView(:_didSelectRowAtIndexPath)

```



然后又出现了新的类以及新概念UIAlertController类和closure




