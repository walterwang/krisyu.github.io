#Taylor Swift系列之八

###理一下

看Working with Table Views的前两篇就很晕，晕乎乎的....

然后想了一下，其实就建了两个类，然后建了好几个ViewController...

那么从头梳理一下：// 啊,其实它每章头上都有learning object

- Build a Basic UI // auto layout related issue ,几个组件可以做stack（感觉群组）,各种intrinsic size , UI搭好
- Connect the UI to Code // outlet, action, delegate , 用action来处理label outlet的属性不难，不过处理textField还是蛮难的，因为有代理，添加代理相应的协议之后，需要再在viewDidLoad中声明代理，还有设计模式以及resignFirstResponder()等高端|||
- Work with View Controllers // 添加了imageView，然后用Gesture Recognizer来处理添加照片，同样要用代理UIImagePickerControllerDelegate，这里跟之前textField不同的地方是这里的delegate声明是放在action函数内，然后再用了两个代理中的方法来实现选中图片present，还有presentViewController这种高端的东西出现
- Implement a Custom Control // 这一小节的learning objective总结的特别好，Create and associate custom source code files with elements in a storyboard，Define a custom class，Implement an initializer on a custom class，Use UIView as a container，
Understand how to display views programmatically，对我来说，这一节很难。
- Define Your Data Model // 新建了一个类，无需有任何继承，所以就直接新建了Swift文件，然后就写了一个failable constructor，它叫的是initializers,然后注意这里把import Foundation改成了import UIKit
- Create a Table View //新建了MealTableViewCell.Swift和MealTableViewController.swift，一个负责展示和管理单个cell，一个负责管理table view,继承自UITableViewController的MealTableViewController自带delegate，使用
-  Implement Navigation // embed in navigator并不难，但是加上segue，还有传递参数又要开始晕了....


###OOP

其实动脑想一下，迄今为止做的事就是：

View:
建立了两个界面(scene)，一个是table view，一个具体每个cell要展示的，这是View.当然，还有各种，比如rating的那个也算一个UIView来做container.

Control:
每个对应的View对应的controller.

Model:自己建了一个class，food的class（这是model的意思么？）,觉得很直观，就像用excel表格来记录食物一样，很直观的（？），就会想spreadsheet来展示一个概况，然后点开则可以看细节。用一个class来记录，然后用不同的方式来展示也很intuitive.



整个UI就是的确属于intuitive的,是因为用iPhone还是因为什么，为什么就直观的想到是这样的呢：就是这样的table view，然后点击其中一个cell，带给我更详细的信息:

```

						+----+      +----+
						|    +----->+    |
						+----+      |    |
						|    |      |    |
						+----+      |    |
						|    |      |    |
						+----+      +----+

```

然后为了完成这些，我们需要掌握的太多，MVC，target-control，delegate，当然，同时，这个教程还没结束，还有更棒的数据存储，和一些table view常用的方法和行为.

理一下不代表我掌握，只有真正开始做一个自己的，才会再翻翻看笔记，然后模仿/copy/改写代码吧。