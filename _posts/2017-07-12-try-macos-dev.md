---
layout: post
title: "macos开发"
---


Apple 统一的非常明显，现在创建macos App,不像以前还可以勾选是否 use storyboard，这件事肯定会对已经用习惯xib的developer造成一些麻烦（？），好吧，其实我也不懂，但是因为这个改变，带来的一些包括，网上的一些教程会不太实用，特别关于 menubar app，还有一些情况就是发现下载下来的project用的全是xib也会有一些略微迷茫的部分。

所以关于menubar app一个简单地解决方案就是去storyboard中把window controller 那个 is initial controller给去掉，这样会有一个warning，也是一种不是办法的办法||||

[How to hide the initial window on start with OS X storyboards](https://stackoverflow.com/questions/27999177/how-to-hide-the-initial-window-on-start-with-os-x-storyboards) 如最高票所示。

iOS已经足够好玩和有意思了，而macos更胜，除了基本与iOS差不多的配置以外，像NSTextView的属性比UILabel更多，Metal run起来更6，还可以写screensaver，还有很多奇技淫巧，run shell，用js来开发，然后套壳，比如atom...