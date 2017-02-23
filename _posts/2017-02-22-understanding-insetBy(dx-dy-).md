---
layout: post
title: "理解 insetBy(dx:dy:)"
---

# 理解 insetBy(dx:dy:)

首先 inset 的意思是嵌入，插入。

它的[API页面在此](https://developer.apple.com/reference/coregraphics/cgrect/1454218-insetby).


> Returns a rectangle that is smaller or larger than the source rectangle, with the same center point.


所以返回的是同中心，然后更大或者更小的rectangle.


关键神奇之处在这里， 这里放入的 dx 或者 dy 可以放正，负，零。看文档：

> dx
The x-coordinate value to use for adjusting the source rectangle. To create an inset rectangle, specify a positive value. To create a larger, encompassing rectangle, specify a negative value.


所以文档的意思就是如果传入 dx = 0， dy = 0， 那么就是与原本的 rectangle 一样的，如果放入负的，则是更大的 rectangle。


> let preheatRect = visibleRect.insetBy(dx: 0, dy: -0.5 * visibleRect.height)
> 


这样创造的 preheatRect 则是原本的 visibleRect 的宽相同的，但是高我们可以用这个新的来 `print(preheatRect.maxY)` 和 `print(preheatRect.minY)` 来看。


或者直接 `print(preheatRect)`，得到矩形的 x, y, width, height.

实际上测试可以发现以上的 preheatRect 代码得到的是与 visibleRect 等宽，高为两倍，同中心的矩形。



