---
layout: post
title: "UIImage Extension实现播放gif"
---


#UIImage Extension实现播放gif

大神写的库中取出一段代码都可以写成另一个库，大神回答的一个stackoverflow问题都可以引出一个库。


读此篇文章有感 → [Swift 玩转gif](http://www.jianshu.com/p/b60a06bdb375)

这篇文章在尝试理解大名鼎鼎的Kingfisher库，而且我只读了其中前半段|||


iOS 的 camera roll是不支持gif显示的。如果我们想加载gif，可选：

- webview
- 第三方库

结果发现其实自己写一个也 so easy，妈妈再也不用担心我的动图不动了。所以实现步骤是：

1. gif 转成 Data
2. 从 Data 中获取 CGImageSource
3. 获取帧数
4. 根据帧数获取每一帧对应的 UIImage 对象和时间间隔
5. 循环播放



然后发现了一个库 [SwiftGif](https://github.com/bahlo/SwiftGif)， 其实做的"差不多"就是这件事：

1. 找出每帧的持续时间
2. 找到最大公因数
3. 根据最大公因数把相应的帧添加到array里面去
4. 根据这个array来创建动画的UIImage


文章的办法比较简单，呈现 gif as it is. 而 SwiftGif 可能会是会在显示方面有所优化（其实我不懂啊\|\|\|。



### 动起来

然后我还顺手研究了一下 NSImageView，要xi了，居然NSImageView这么简单，只要把animates属性设置为true就可以了|||

这一切让我有点不敢相信 UIImageView，转回去再看了几眼确定它是不直接支持 gif 播放的。

### Talk is cheap


所以就模仿SwiftGif写了一个 extension,然后就可以直接用了

[UIImage Extension to show Gif](https://github.com/KrisYu/SwiftExtensions/blob/master/GifExt.swift)



感觉也可以 marketing 一下啊 \|\|\|