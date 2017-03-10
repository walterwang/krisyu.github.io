---
layout: post
title: "最简单的GCD"
---

# 最简单的GCD

对GCD非常印象深刻的一次是加载网络数据（还是本地文件？）到 tableView 中，然后可能文件有一定大小，运行不出结果。然后就一直debug，debug，debug，直到崩溃\|\|\|,直到稍等了一下，那才算是第一次认识GCD吧。

今天又重新认识了GCD，把一个耗时的工作放在了 viewDidLoad中，原来它是真的会block UI thread的，因为直到这个操作做完了，才出现我的 Navigation Controller，而使用异步操作就OK.

所以还是要用老爷爷讲的：

- let mainQ: dispatch\_queue\_t = dispatch\_get\_main\_queue()- All UI stuff must be done on this queue!- And all time-consuming (or, worse, potentially blocking) stuff must be done off this queue!
- Common code to write ...


```dispatch_async(not the main queue) {// do a non-UI that might block or otherwise takes a while      dispatch_async(dispatch_get_main_queue()) {// call UI functions with the results of the above} }
```


Swift 3.0 的写法


```
DispatchQueue.global().async {
    // do a non-UI that might block or otherwise takes a while    DispatchQueue.main.async {
        // call UI functions with the results of the above
        }
}
```

这就是最简单的处理异步操作用的办法（看到别人创建各种queue，各种dispatch),也是我最爱用的，因为更复杂的我也不会\|\|\|