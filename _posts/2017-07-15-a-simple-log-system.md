---
layout: post
title: "设计一个极简的log系统"
---

在 macOS/iOS 中，存储如果就依靠原生系统的存储，一般有三个选项：

- UserDefaults :  key-value的配对，一般存一点比较简单的全局设置
- plist :  xml，存一点dictionary，array之类的比较适合
- core data ： object啥的

因为模（zhao）仿（chao）一个macOS番茄钟，想给它加上一个log功能，觉得这个用plist应该就够了，然后觉得应该不会很难。

1. App finish launching的时候从plist中读取当日已经完成的个数，然后显示在App里。这里又分两种情况：
   - 存在plist文件，直接读取
   - 第一次使用or plist文件不存在，那么这个时候就创建一个plist文件，并且写入当天完成个数为0

2.App 要退出的时候把当天更新完成的番茄钟个数写入

简单也足以完成功能，值得注意的是存在好写Dictionary 与 NSDictionary的转换是因为writetoFile是NSDictonary特有的。

show me the code:

<script src="https://gist.github.com/KrisYu/b94f79ad3d356d7e7f20356e467aeed3.js"></script>


