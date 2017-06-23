---
layout: post
title: Working with xib Files
---


之前在GitHub上下了一个mac osx app repo，然后发现代码结构居然跟我想的不太一样，因为现在如果新建mac osx application，直接就会默认使用storyboard，然后会生成很多东西。

很多用ObjC的repo也是： 用.xib，然后outlet连接在APPDelegate里面，研究了一会才发现如何做到的。

mark在此：

1. 删除 storyboard
2. 新建一个User Interface - Application, 这个里面自带 Menu 和 Window
3. 去General里面更改 Main Interface 为 Application.xib
4. 拖拽一个Object扔去 Main Menu上面
5. 把这个Object的名字改成App Delegate
6. 最上层的Placeholders里去outlet把它跟刚刚的App Delegate连起来。


此处有配图版本：

[Working with .xib Files](https://developer.xamarin.com/guides/mac/application_fundamentals/working-with-xibs/)

参见第 11 - 15步以及其配图。



