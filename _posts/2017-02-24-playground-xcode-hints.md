---
layout: post
title: "玩Playground的几个点"
---

# 玩Playground的几个点

 - playground 里面如果全局域用`guard let else { return }` 会报错，因为全局不建议用return，用`exit(1)` 就可以解决问题。

- Bundle是算"应用程序包"，存放应用程序的源文件，资源文件和可执行文件，所以如果我们一般放在 playground resource 文件夹里面的或者xcode项目里面放的东西就可以直接

可以通过以下调用：

`let filePath = Bundle.main.path(forResource: _, ofType: _)` 

- Documents是最常用的目录，iTunes同步该应用时会同步此文件夹中的内容，适合存储重要数据。 

这样来得到：

`let docDir = NSSearchPathForDirectoriesInDomains(.documentDirectory, .userDomainMask, true).`


- filePath 和 fileURL 是不同的东西

可以作用于 fileURL 上的方法貌似更多，之前已经得到了filePath，转成NSURL

`let fileURL = NSURL(fileURLWithPath: filePath!)`

比如我们可以通过 fileURL 的方法 `fileURL.lastPathComponent` 获得文件名。




- playground 使用异步方法

```
import PlaygroundSupport

PlaygroundPage.current.needsIndefiniteExecution = true
```

