---
layout: post
title: "把App发布到App Store以外的地方"
---


keywords: Mac App, macOS, Swift, Distribute, Developer


继续上篇，来尝试发布App吧，先尝试发布到别的地方（App Store还有待研究。要实现这一步，需要你有developer账号。

为啥需要这样做呢，因为有这个

![]({{site.baseurl}}/images/menubar/08.png)


不过感觉还是要App Store化


### 开始

首先去`project navigator`， 选择sign in


然后我们需要`Create Developer ID Certificates`，如果你还没有这个的话，去<developer.apple.com/account> 创建一个，然后下载下来，加到钥匙串里面就可以了。（我非常惊讶自己做过这件事，因为之前搞不太懂，居然电脑上已经有


我的这个跟它截屏虽然不太一样，已经做好了要出错的心理准备。


结果跟着文档开始创建Archive的时候一路通畅下来，居然没有问题。

至此，顺利打包完成。


### 安装disk

然后我就想把它变成常见的安装dmg.


发现原来也很简单，用`disk utility`创建一个新的disk，mount把 app 和给 Applicaiton 制作的 alias 拷贝进去。

然后再把制作的dmg用 disk utility再转一次变成 readonly 的 dmg，就和别人的发布一样了。


![]({{site.baseurl}}/images/menubar/07.png)


其实zip app也一样OK


参考：


[Distributing Apps Outside the Mac App Store](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/DistributingApplicationsOutside/DistributingApplicationsOutside.html)

[Creating Signing Identities](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html#//apple_ref/doc/uid/TP40012582-CH31-SW6)


[Creating a "DMG installer" for OS X](https://gist.github.com/jadeatucker/5382343)

